---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: true
created: 2025-02-06T14:56
updated: 2025-02-06T19:20
---
PECS è l'abbreviazione di ***Producer extends Consumer super*** ed indica il principi che regola l'utilizzo del operatore jolly dove, che:
- per i **Producer** (lettore), ovvero metodi ed oggetti che effettuano operazioni di lettura su collezioni generiche, si utilizza `extends`,
- per i **Consumer** (scrittore) ovvero metodi ed oggetti che effettuano operazioni di scrittura su collezioni generiche, si utilizza`super`.  

## Extends

Quando ad un operatori jolly `?` è associato l'operatore `extends` di una classe `X` stiamo dicendo che il tipo è limitato alla classe `X` o a dei sui **sottoclassi** (classi che estendono `X`).

>[!note] Lettura
>
>```java
>public static void StampaMele(`List<? extends Mela> lista) {  
>    for (Mela mela : lista)               // va bene (1)  
>        System.out.println(mela);  
>  
>    for (Frutto frutto : lista)           // va bene (2)  
>        System.out.println(frutto);  
>
>    for (MelaMelinda melaMelinda : lista) // errore di compilazione (3)  
>        System.out.println(melaMelinda);  
>
>    for (Pera pera : lista)               // errore di compilazione (4)  
>        System.out.println(pera);     
>}
>```
>
>- (1) e (2) non danno errori di compilazione perché siamo sicuri che la lista è composta da mele o da delle sotto classi di mela (e quindi da frutti)
>- (3) e (4) da errore di compilazione perché non possiamo essere sicuri che la classe contenga MeleMelinda (sottoclasse di Mela) o Pere

>[!note] Scrittura
>
>```java
>public static void AggiungiMela(`List<? extends Mela> lista) {
>    lista.add(new Mela());        // errore 
>    lista.add(new MelaMelinda()); // errore
>    lista.add(new Frutto());      // errore  
>    lista.add(new Object());      // errore
>}
>```
>
>- (1) e (2) danno errori di compilazione perché il compilatore non può garantire che la lista sia effettivamente di tipo Mela o suoi sottotipi.
>- (3) e (4) danno errori di compilazione perché non possiamo inserire un frutto o oggetto qualsiasi in una lista di mele o di sui sottotipi.

## Super

Quando ad un operatori jolly `?` è associato l'operatore `super` di una classe `X` stiamo dicendo che il tipo è limitato alla classe `X` o alle sue **superclassi**.

>[!note] Lettura
>
>```java
>public static void StampaMele(`List<? super Mela> lista) {  
>    for (Mela mela : lista)         // errore (1)
>        System.out.println(mela);
>        
>    for (Object obj : lista)        // va bene
>		System.out.println(obj);
>}
>```
>
>- (1) da errore di compilazione nel `for` perché non siamo sicuri che la lista contenga mele infatti potrebbe contenere degli oggetti super-classe di mela (come frutto o object) e non solo mele.
>- (2) l 'unico modo per non avere errori di compilazione è utilizzare `Object` come tipo di iterazione, infatti indipendentemente da tipo di oggetto contenuto dalla lista siamo sicuri che sia un `Object`.

>[!note] Scrittura
>
>```java
>public static void AggiungiMela(`List<? super Mela> lista) {  
>	lista.add(new Mela());        // va bene (1)
>	lista.add(new MelaMelinda()); // va bene (2)
>	lista.add(new Frutto());      // errore  (3)
>}
>```
>
>- (1) e (2) sono corretti perché la lista potrebbe essere di Mela o di super-classi come Frutto o Object, e quindi il down-casting è ammesso.
>- (3) non va bene perché se la lista è di Mela, allora non possiamo inserire un Frutto (up-casting). Questo è perché il tipo di lista è specificato come super-classe di Mela, quindi possiamo solo aggiungere oggetti di tipo Mela o suoi sottotipi.