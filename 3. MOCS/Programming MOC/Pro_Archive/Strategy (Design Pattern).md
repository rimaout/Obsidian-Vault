---
type: Programming Note
programming language: "[[Java MOC]]"
related:
  - "[[Software Design Pattern]]"
  - "[[Metodologie di Programmazione (class)]]"
completed: false
created: 2024-07-09T15:38
updated: 2024-07-10T19:31
---
>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Funzionamento]]
>3. [[#Esempio]]

>[!abstract] Related
>- [[Software Design Pattern]]
>- [[Metodologie di Programmazione (class)]]
>- [[Java MOC]]

---
## Introduzione

**Strategy** è un design pattern comportamentale che permette di definire una famiglia di algoritmi, metterli ciascuno in una classe separata e rendere i loro oggetti interscambiabili.

>[!note] Intercambialità
>Rendere degli algoritmi intercambiabili significa che è possibile sostituire un algoritmo con un altro della stessa famiglia senza modificare il contesto che utilizza l'algoritmo. Quindi la tipologia di Input e Output, e la logica interna degli algoritmi deve essere consistente.
^096caa

---
## Funzionamento

![[umlstrategy.png|500]]

|                          |                                                                                                                                             |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------- |
| **Context**              | La Classe che utilizza l'oggetto `strategy`. In particolare è responsabile della gestione degli `input` e `output` dell'oggetto `strategy`. |
| **Strategy (Interface)** | L'interfaccia che definisce il contratto (ovvero l'algoritmo generale) che le strategie concrete devono eseguire.                           |
| **Concrete Strategies**  | Le classi che implementano l'Interfaccia `Strategy`. Ogni strategia concreta fornisce una implementazione specifica dell'algoritmo.         |
| **Client**               | La lasse che utilizza la classe `Context`. È la classe che inizia l'esecuzione dell'algoritmo chiamando la classe di contesto.              |

---
## Esempio

Questo esempio consiste nell'implementazione dei metodi utilizzati per effettuare dei pagamenti all'interno di un app.

Partiamo da uno [[#Stato iniziale]] dove non viene applicato lo **Strategy Pattern**, 
### Stato iniziale

Partiamo dallo [[#Stato iniziale]] dove tutto è in unica classe, in questo caso questo metodo si occupa sia dei pagamenti via carta di credito che via PayPall.

>[!note] Codice
>```java
>public public class PaymentService {
>    private int cost;
>    private boolean includeDelivery; 
>
>    public void procceesPayment(String paymentMethod){
>        if("CreditCard".equals(paymentMethod)){
>            // pop-up to collect credit card info
>            // process payment
>            System.out.println("Paying " + getTotalCost() + " with Credit Card");
>        } else if("PayPal".equals(paymentMethod)){
>            // pop-up to collect PayPal info
>            // process payment
>            System.out.println("Paying " + getTotalCost() + " with PayPal");
>        }
>    }
>
>    public int getTotalCost(){
>        return cost + (includeDelivery ? 10 : 0);
>    }
>}
>```

>[!danger] Problemi
>- Codice poco leggibile
>- Difficile da mantenere infatti aggiungere altri metodi di pagamento, richiede di modificare un metodo funzionante rischiando di inserire dei bug. In particolare inserire un altro metodo di pagamento in questo codice significherebbe estendere la catena di `if else`.
>- Non rispetta il [[Open/Closed Principle]].
>- Non rispetta il [[Single Responsibility Principle]].

### Applicare Strategy Pattern

>[!danger] Soluzione
>1. Definiremo un'interfaccia comune, `PaymentStrategy`, per tutti i metodi di pagamento.
>2. Implementeremo classi concrete di metodi di pagamento che aderiscono a questa interfaccia. 
>	- Nota bene facendo ciò rendiamo le classi che implementano i metodi di pagamento [[#^096caa|intercambiabili]] tra loro.
>3. Creeremo una classe di contesto, `PaymentService`, che utilizza l'interfaccia `PaymentStrategy` per elaborare i pagamenti.

#### 1) Creazione dell'interfaccia Strategy 

Per rendere le classi dei metodi di pagamento intercambiabili quest'ultime dovranno implementare un interfaccia (**Strategy**) che:
- stabilisce la struttura della logica interna delle classi.
- stabilisce gli input e output che le accomunano le classi.

>[!note]- Codice Interfaccia Strategy
>```java
>public interface PaymentStrategy {
>
>    void collectPaymentDetails();
>    boolean validatePaymentDetails();
>    void pay(int amount);
>}
>```

#### 2) Implementazione dell'interfaccia Strategy

Dopo aver definito l'interfaccia, dobbiamo assicurarci che venga implementata nelle classi dei metodi di pagamento.

>[!note]- Codice dei metodi che implementano interfaccia (Concrete Strategy)
>```java
>public class PaymentByCreditCard implements PaymentStrategy {
>
>    private CreditCard card;
>
>    @Override
>    public void collectPaymentDetails() {
>        // Pop-up to collect card details...
>        card = new CreditCard("cardNumber", "expiryDate", "cvv");
>        System.out.println("Collecting Card Details...");
>    }
>
>    @Override
>    public boolean validatePaymentDetails() {
>        // Validate credit card...
>        System.out.println("Validating Card Info: " + card);
>        return true;
>    }
>
>    @Override
>    public void pay(int amount) {
>        System.out.println("Paying " + amount + " using Credit Card");
>        card.setAmount(card.getAmount() - amount);
>    }
>
>}
>```
>
>```java
>public class PaymentByPayPal implements PaymentStrategy {
>
>    private String email;
>    private String password;
>
>    @Override
>    public void collectPaymentDetails() {
>        // Pop-up to collect PayPal mail and password...
  >      email = "PayPal Mail";
>        password = "PayPal Password";
>        System.out.println("Collecting PayPal Account Details...");
>    }
>
>    @Override
>    public boolean validatePaymentDetails() {
>        // Validate account...
>        System.out.printf("Validating PayPal Info: %s | %s%n", email, password);
>        return true;
>    }
>
>    @Override
>    public void pay(int amount) {
>        System.out.println("Paying " + amount + " using PayPal");
>    }
>
>}
>```

#### 3) Implementazione del classe Context

Una volta implementata l'interfaccia Strategy, possiamo utilizzarla nel classe di contesto ovvero la classe che utilizza l'interfaccia Strategy, in questo caso `PaymentService`. 

>È importante notare che questo metodo oramai non ha più visibilità sul come la logica di pagamento avvenga, infatti questa responsabilità è stata delegata a tutti i metodi che implementano l'interfaccia strategy.
>
>Questo è importante perché ci permette di implementare altri metodi di pagamento senza dovere toccare il resto del codice.

>[!note]- Codice classe Context
>```java
>@Setter
>public class PaymentService {
>
>    private int cost;
>    private boolean includeDelivery = true;
>
>    private PaymentStrategy strategy;
>
>    public void processOrder(int cost) {
>        this.cost = cost;
>        strategy.collectPaymentDetails();
>        if (strategy.validatePaymentDetails()) {
>            strategy.pay(getTotal());
>        }
>    }
>
>    private int getTotal() {
>        return includeDelivery ? cost + 10 : cost;
>    }
>
>}
>```

#### Esempio di utilizzo (client)

Vediamo un esempio di un possibile `client` che utilizza le classi utilizzate per implementare `PaymentService` utilizzando lo `Strategy Pattern`.

>[!note] Esempio Client
>```java
>public class Main {
>    public static void main(String[] args) {
>        // Creo un oggetto PaymentService
>        PaymentService paymentService = new PaymentService();
>
>        // Utilizzo la strategia di pagamento con carta di credito
>        paymentService.setStrategy(new PaymentByCreditCard());
>        paymentService.processOrder(100);
>
>        // Utilizzo la strategia di pagamento con PayPal
>        paymentService.setStrategy(new PaymentByPayPal());
>        paymentService.processOrder(200);
>    }
>}
>```

---

>[!info] Sources
>- https://www.youtube.com/watch?v=Nrwj3gZiuJU
>- https://refactoring.guru/design-patterns/strategy
