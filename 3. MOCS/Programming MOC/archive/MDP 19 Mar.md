---
created: 2024-03-19
type: Programming Note
programming language: "[[Java MOC]]"
related: 
completed: false
updated: 2024-05-27T13:29
---
---

>[!info] Index
>1. 

---
## copyOf (arrays)
copyOf metodo statico della classe java.util.Arrays

---
## Metodi con numero variabili di argomenti 

`type ..`

Example:

```java
public static double sum(double...) 
```

>[!warning] oss
>- Ci può essere una sola sequenza di parametri variabili (deve essere posizionata come ultimo parametro)
>- Se sono presenti altri parametri devono essere dichiarati prima della sequenza 

---
## Array a due dimensioni 


Gli elementi della matrice vengono inizializzati al valore di default del tipo della matrice 

---
## Metodi setX() getX()


---
## Campi statici 

![[Pasted image 20240319095046.png|800]]

---
## Enumerazioni

- In java esistono le classi e poi le enumerazione 
- Le enumerazioni contengono delle costanti enumerative

Esempio:
![[Pasted image 20240319095640.png|500]]

Come altre classi possono avere:
- costruttori
- campi
- metodi

Esempio:
![[Pasted image 20240319095756.png|500]]

![[Pasted image 20240319100626.png|700]]

---
## Metodi values() e valuesOf()
- values of è un metodo statico che ci permette data un enum di ottenere un riferimento public final che coincide con ... 


---
## Enum e switch 

![[Pasted image 20240319101402.png|800]]

---
## Classi wrapper

- permettono di convertire i valori primitivi in un oggetto 
- forniscono metodi di accesso e visualizzazione dei valori 

![[Pasted image 20240319101837.png|700]]

>[!warning] oss
>per confrontare due oggetti si usano:
>- equals()
>- compareTo()

>[!danger] Costo di un oggetto rispetto a un primitivo
>.Un oggetto qualsiasi costa minimo 8 byte
>- Informazioni di base come la classe dell'oggetto, flag di status, ID, ecc.
>- Un Integer 8 byte dell'oggetto + 4 byte per l'int + padding = 16 byte
>- Un Long 8 + 8 = 16 byte!
>- Un riferimento "costerebbe" 8 byte, ma si usano i `compressed oop` (ordinary object pointer) che sono object offset da 32 bit (ogni 8 byte), quindi indicizzano fino a 32Gb di RAM (attivi fino a – Xmx32G), quindi richiedono normalmente 4 byte

---
## Auto-boxing e Auto-unboxing

**Auto-boxing:** 

**auto-unboxing:**

---
## Ereditarietà

Ereditarietà concetto utilizzato nella metodologia "mattone su mattone" 

**Estendere una classe:**
- Una sottoclasse estende la super-classe
- La sottoclasse eredita i membri della super-classe
- Campi e metodi d’istanza secondo il livello

>[!warning] oss
>Inoltre la sottoclasse può:
>- aggiungere nuovi metodi e campi
>- ridefinire i metodi che eredita dalla super-classe (tipicamente NON i campi)

---
## Astrazione 

### Classi astratte
Serve a definire delle classi che posso riutilizzare come basi per altre classi
- una classe astratta non può essere utilizzata per creare un oggetto
- Ma può essere ereditata da altre sotto classi

### Metodi astratti 


### Super keyword

![[Pasted image 20240319114915.png|700]]

---
## UML ereditarietà


---

