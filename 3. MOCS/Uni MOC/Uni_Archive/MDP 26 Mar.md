---
Created: 2024-03-26
Type: Uni Note
Class:
  - "[[Metodologie di Programmazione (class)]]"
Academic Year: 2023/2024
Related: 
Completed: false
---
---

>[!info] Index
>1. 

---

## Polimorfismo

### Binding 

>[!note] Definition
>Binding è il processo di associare un tipo ad una variabile, funzione o altro

java è un linguaggio compilato, il compilatore stabilisce, in maniera statica ovvero non a tempo di esecuzione, il tipo delle variabili 

### Binding dinamico

Lavoro che viene effettuato in real time (durante il tempo di esecuzione) dove ...

### Binding statico


### @override
permette di riscrivere un metodo esistente in una per classe rispettando il suo input e output

---
## String Buffer


---
## Super per chiamare metodi
Super permette di fare due cose
1. Chiamare costruttore della super classe
2. Un metodo della super classe

**Esempio:**
![[Pasted image 20240326101439.png|800]]

---
## is instance of


---
## Up-casing


---
## Down-Casting


---
## Classe object

![[Pasted image 20240326111512.png|600]]

---
## Ri implementare il metodo `equals`
- Il metodo equals viene invocato per confrontare il contenuto di due oggetti

>[!warning] oss
>Per default, se sono “uguali”, il metodo restituisce true
>```java
>public boolean equals(object o){ return this == 0}
>```
 
**Equals di default non tiene conto del contenuto delle sotto classi:**
- per mantenere il "contratto" del metodo è necessario sovrascriverlo 
	![[Pasted image 20240326113143.png|700]]

---
## Classe Object 

- Object è la superclasse di tutte le classi
- Ogni classe è automaticamente un estensione (sottoclasse di equals)

>[!note] Metodi di equals 
