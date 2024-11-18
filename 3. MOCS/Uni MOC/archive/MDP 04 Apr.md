---
created: 2024-04-04
type: Uni Note
class:
  - "[[Metodologie di Programmazione (class)]]"
academic year: 2023/2024
related: 
completed: false
updated: 2024-05-27T13:29
---
---

>[!info] Index
>1. 

---
## Interface
- Esse specificano soltanto il comportamento che un certo oggetto deve presentare all'esterno
- le interfacce non forniscono le implementazione dei metodi


oss: le interfacce sono classi astratte

**Metodi di default:**
- è possibile specificare delle implementazioni di default di metodi non statici

oss: il polimorfismo per metodi statici non è possibile

###### Cosa sono
Un’interfaccia di fatto è una classe che può contenere soltanto:
- costanti
- metodi statici 
- implementazioni di default (java 8)
- metodi privati (java 9)

>[!warning] oss
>- Tutti i metodi dichiarati in un’interfaccia sono implicitamente public abstract  
>
>- Tutti i campi dichiarati in un’interfaccia sono implicitamente public static final
> 
>- Tranne nel caso dei metodi di default o statici, non è possibile specificare alcun dettaglio implementativo
> 
>	-  non vi è alcun corpo di metodo o variabile di istanza

**Esempio 1:**


**Esempio 2:**


### Modellazione di comportamenti comuni 
Le interfacce permettono di modellare comportamenti comuni a classi che non sono necessariamente in relazione gerarchica (is-a, è-un)

**Esempio:**

![[Pasted image 20240404122607.png|630]]

![[Pasted image 20240404122833.png|600]]

![[Pasted image 20240404123821.png|600]]

![[Pasted image 20240404123713.png|600]]

---
## Iterable 
Interfaccia standard che si trova in `java.lang` che ci permette di 


## Iterator
- E’ un’interfaccia fondamentale che permette di iterare su collezioni
- si triv in `jave.utils`

**Tre metodi:**
- hasNext()
- next()
- remove()

**Esempio:**
per creare una stinga iterabile `Iterable<Character>`

