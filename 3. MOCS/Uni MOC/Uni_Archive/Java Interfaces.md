---
type: Uni Note
class: 
academic year: 2023/2024
related: 
completed: true
created: 2024-06-17T15:30
updated: 2024-08-11T18:07
---
>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Implementazione]]
>3. [[#Metodi Default e Statici]]
>4. [[#Eredità Multipla]]
>5. [[#Estendibilità]]
>6. [[#Interfacce Funzionali]]

>[!abstract] Related
>- [[Java MOC]]
>- [[Metodologie di Programmazione (class)]]

>[!danger] TLDR
>Un'interfaccia specifica un insieme di metodi che una classe deve implementare se vuole implementare quell'interfaccia

---
## Introduzione 

In Java, un'interfaccia è un tipo di riferimento che può contenere solo:
- **Metodi astratti**
- **Campi costanti** (che sono implicitamente `public`, `static`, e `final`

 Le interfacce vengono utilizzate per definire un contratto che deve essere implementato da una classe concreta. In altre parole, una classe che implementa un'interfaccia deve fornire una implementazione per tutti i metodi definiti nell'interfaccia.

>[!note] Esempio
>```java
>java
>public interface FormaGeometrica {
>   double PI = 3.14;
>   double area();
>   double perimetro();
>}
>```

---
## Implementazione

Implementare un interfaccia significa creare una classe che implementa i metodi (astratti) contenuti dall'interfaccia

>[!note] Esempio
>```java
>public class Cerchio implements FormaGeometrica {
>   private double raggio;
>   
>   public Cerchio(double raggio) {
>      this.raggio = raggio;
>   }
>   
>   @Override
>   public double area() {
>      return PI * raggio * raggio;
>   }
>   
>   @Override
>   public double perimetro() {
>      return 2 * PI * raggio;
>   }
>}
>```
>In questo esempio, abbiamo definito una classe `Cerchio` che implementa l'interfaccia `FormaGeometrica`. La classe `Cerchio` deve fornire una implementazione per i metodi `area()` e `perimetro()` definiti nell'interfaccia.

### Metodi Default e Statici 

Le interfacce possono anche contenere metodi di default e statici, che possono essere implementati direttamente nell'interfaccia stessa. 

>[!warning] Metodi di Default
>Definendo metodi con implementazione di default all'interno delle interfacce diamo la libertà a chi implementa l'interfaccia di scegliere se sovrascrivere il metodo di default o utilizzare l'implementazione predefinita.

>[!warning] Metodi Statici
>Definendo metodi statici all'interno delle interfacce. Questi metodi possono essere chiamati utilizzando il nome dell'interfaccia seguito dal nome del metodo.

>[!note] Esempio
>```java
>public interface FormaGeometrica {
>   double PI = 3.14;
>   
>   default double areaCirconferenza(double raggio) {
>      return PI * raggio * raggio;
>   }
>   
>   static double areaQuadrato(double lato) {
>      return lato * lato;
>   }
>   double area();
>   double perimetro();
> }
>```

---
## Eredità Multipla

Java supporta l'ereditarietà multipla tramite le interfacce. Una classe può implementare più di un'interfaccia, consentendo così di ereditare comportamenti da più fonti.

Tuttavia, Java non supporta direttamente l'ereditarietà multipla per le classi. Ciò significa che una classe in Java può estendere solo una singola classe base. Tuttavia, Java supporta l'ereditarietà multipla indiretta attraverso l'utilizzo di interfacce.

>[!note]- Esempio
>```java
>public interface Forma {
>   double PI = 3.14;
>   double area();
>}
>
>public interface Stampabile {
>   void stampa();
>}
>
>public class Cerchio implements Forma, Stampabile {
>   private double raggio;
>   
>   public Cerchio(double raggio) {
>      this.raggio = raggio;
>   }
>   
>   @Override
>   public double area() {
>      return PI * raggio * raggio;
>   }
>   
>   @Override
>   public void stampa() {
>      System.out.println("Stampo il cerchio con raggio " + raggio);
>   }
>}
>```

---
## Estendibilità

Le interfacce possono estendere altre interfacce, consentendo la creazione di gerarchie di interfacce. Una classe che implementa un'interfaccia estesa deve fornire implementazioni per tutti i metodi definiti nelle interfacce padre.

>[!note]- Esempio
>
>```java
>
>public interface Forma {
>   double PI = 3.14;
>   double area();
>}
>
>public interface Stampabile {
>   void stampa();
>}
>
>public interface FormaStampabile extends Forma, Stampabile {
>   double perimetro();
>}
>
>public class Cerchio implements FormaStampabile {
>   private double raggio;
>   
>   public Cerchio(double raggio) {
>      this.raggio = raggio;
>   }
>   
>   @Override
>   public double area() {
>      return PI * raggio * raggio;
>   }
>   
>   @Override
>   public void stampa() {
>      System.out.println("Stampo il cerchio con raggio " + raggio);
>   }
>   
>   @Override
>   public double perimetro() {
>      return 2 * PI * raggio;
>   }
>}
>```
>
>In questo esempio, l'interfaccia `FormaStampabile` estende le interfacce `Forma` e `Stampabile`, il che significa che una classe che implementa `FormaStampabile` deve fornire implementazioni per i metodi astratti `area()` e `stampa()` ereditati da `Forma` e `Stampabile`, nonché per il metodo astratto `perimetro()` definito in `FormaStampabile`.

---
## Interfacce Funzionali

Le interfacce funzionali sono un tipo speciale di interfacce che hanno un solo metodo astratto, che può essere implementato come una funzione lambda. Queste interfacce sono anche note come interfacce a singolo metodo o SAM (Single Abstract Method) interfaces.

Le interfacce funzionali sono state introdotte per semplificare l'uso delle funzioni lambda in Java, che sono blocchi di codice anonimi che possono essere passati come argomenti a metodi o assegnati a variabili. Le funzioni lambda possono essere utilizzate per creare oggetti che implementano interfacce funzionali, il che può semplificare il codice e renderlo più conciso ed espressivo.

>[!note]- Esempio
>```java
>
>@FunctionalInterface 
>public interface Calcolatrice {    
>	int calcola(int a, int b); 
>} 
>
> public class Main {    
>	public static void main(String[] args) {       
>		Calcolatrice somma = (a, b) -> a + b;       
>		Calcolatrice differenza = (a, b) -> a - b;              
>		System.out.println("Somma: " + somma.calcola(5, 3));       
>		System.out.println("Differenza: " + differenza.calcola(5, 3));    
>	}
>}
>```
>
>In questo esempio, l'interfaccia `Calcolatrice` è una interfaccia funzionale che definisce un metodo astratto `calcola()` che prende due argomenti interi e restituisce un intero. Nella classe `Main`, creiamo due oggetti `Calcolatrice` che implementano il metodo `calcola()` come funzioni lambda. Questo ci permette di creare oggetti `Calcolatrice` in modo conciso e di utilizzarli per eseguire calcoli semplici.

