---
Created: 2024-04-23
Type: Uni Note
Class:
  - "[[Introduzione agli Algoritmi (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Strutture Dati]]"
Completed: true
---
---

>[!abstract] Index
>1. [[#Definizione]]
>2. [[#Operazioni]]
>3. [[#Appunti Lezione]]

>[!abstract] Related
>- [[Strutture Dati]]
>- [[Introduzione agli Algoritmi (class)]]

---
## Definizione

Un array o vettore è la più semplice struttura dati

---
## Operazioni

##### Search(S, x)
- **Array disordinato:** bisogna scorrere l’array: `O(n)`
- **Array ordinato:** ricerca binaria: `O(n log nx) `

##### Min(S) Max(S) 
- **Array disordinato:** bisogna scorrere l’array: `θ(n)`
- **Array ordinato:** primo o ultimo elemento: `θ(1)`

##### Insert(S, x)
- **Array disordinato:** inserimento di x nella prima posizione libera: `θ(1)`
- **Array ordinato:** ricerca della posizione, scorrimento a destra degli elementi maggiori ed inserimento: `θ(n)`

##### Delete(S, x)
- **Array disordinato:** eliminazione di x e scambio con l’ultimo elemento: `θ(1)`
- **Array ordinato:** eliminazione e scorrimento a sinistra per coprire lo spazio lasciato: `θ(n)`

---
## Appunti Lezione 

Quando dichiariamo un classico array dobbiamo decidere la dimensione che non potrà mai più essere cambiata 

```c
int ANum[50]
```

Se riempiamo la capienza massima dell'array dobbiamo crearne uno nuovo (con dimensione maggiore) ed spostare tutti i dati dal vecchio array al nuovo

Inoltre un classico array può contenere un solo data type, infatti per dichiarare un array dobbiamo specificare un tipo di dato e quanti elementi allocare 

in questo caso ad ogni tipo di dato è associata un dimensione, per esempio un char occupa un byte, quindi quando allochiamo un array di 50 char stiamo allocando $50\cdot 1 \text{ byte}$ nella memoria

---