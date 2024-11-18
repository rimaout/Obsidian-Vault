---
created: 2024-03-07T12:21
type: Uni Note
class: 
academic year: 2023/2024
related: 
completed: false
updated: 2024-05-27T13:29
---
---

>[!info] Index
>1. 

---
In java il tipo string in realtà è una classe, ma ha dei comportamenti particolari e per questo viene considerata come classe speciale 

## Comportamenti "Speciali"
**non serve chiamare un costruttore per inizializzare una stinga**

```
String a = new String('c', 'i', 'a', 'o') 
// non serve

// si può dichiarare come qualsiai altro tipo primitivo
String a = "Ciao"

```

## Metodi 

`.lenght()` 

---
`.toLowerCase()`, `.toUpperCase()`

>[!warning] La stringa originale non viene modificata

---

`.charAt` output char

---

`.substring(startIndex, endIndex)`

esiste anche versione `.substring(startIndex)` ...

>[!warning] La stringa originale non viene modificata

---

`s1.concat(s2)` equivalente a `s1 + s2` ma più efficiente 

Se si devono concatenare parecchie stringhe è bene utilizzare la classe `StringBuilder`

---

`StringBuilder` che contiene `.append(s2)` e `.insert(pos, s2)`

---

`.indexOf(c)` cerca un carattere nella stinga e ritorna la posizione della sua prima occorrenza se non presente ritorna -1

può essere utilizzato per cercare delle stringhe in una stringa `.indexOf(s2)`

---

`.replace8()` utilizzato per sostituire tutte le occorrenze di un carattere o di una stringa

---

Le stringhe (come tutti gli oggetti) vanno sempre confrontare sempre con il metodo `equals`

**Differenza tra equals e \==**
- L'operatore `==` confronta il riferimento (diciamo l'indirizzo in memoria), quindi ritorna `True` solo se si confrontano gli stessi oggetti fisici 
- L'operatore `equals` confronta le stringhe carattere per carattere 

---

`.split()` input espressione regolare [[regex]]

---




---
## Inizializzazione implicita di oggetto 

Al momento della creazione di un oggetto i campi di una classe sono inizializzati automaticamente

![[Pasted image 20240307132048.png|600]]

>[!warning]
>le inizializzazioni sono automatiche  per i campi di una classe ma non per le variabili locali 

---
## Variabili e oggetti 
non esistono variabili che contengono oggetti ma variabili che puntano ad oggetti 

---

## Disegno memoria
1. analizzare campi statici (inserirli nel meta space)
2. poi andare nel main
3. se respinte  presente args in input allora vettore che contiene stringhe
4. se non presenti stinghe args allora vettore vuoto 
5. 
