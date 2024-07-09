---
type: Programming Note
programming language: "[[Java MOC]]"
related:
  - "[[Software Design Pattern]]"
  - "[[Metodologie di Programmazione (class)]]"
completed: false
created: 2024-07-09T15:38
updated: 2024-07-09T22:04
---
>[!abstract] Index
>1. 

>[!abstract] Related
>- 

---
## Introduzione

**Strategy** è un design pattern comportamentale che permette di definire una famiglia di algoritmi, metterli ciascuno in una classe separata e rendere i loro oggetti interscambiabili.

---
## Esempio

Questo esempio consiste nell'implementazione dei metodi utilizzati per effettuare dei pagamenti all'interno di un app.

>**Fonte:** https://www.youtube.com/watch?v=Nrwj3gZiuJU

##### Stato iniziale

Partiamo dallo [[#Stato iniziale]] dove tutto è in unica classe, in questo caso questo metodo si occupa sia dei pagamenti via carta di credito che via paypall.

>[!danger] Problemi
>- Codice poco leggibile
>- Difficile da mantenere infatti aggiungere altri metodi di pagamento, richiede di modificare un metodo funzionante rischiando di inserire dei bug. In particolare inserire un altro metodo di pagamento in questo codice significherebbe estendere la catena di `if else`.
>- Non rispetta il [[Open/Closed Principle]].
>- Non rispetta il [[Single Responsibility Principle]].

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
##### Applicare Strategy Pattern

>[!danger] Soluzione
>- Dobbiamo inserire ogni metodo di pagamento nella sua classe (rendendo ogni classe responsabile per un solo metodo di pagamento)
>- Queste classi devono essere intercambiabili questo significa che devono avere gli stessi input e output 

---

>[!info] Sources
>- https://www.youtube.com/watch?v=Nrwj3gZiuJU
>- https://refactoring.guru/design-patterns/strategy