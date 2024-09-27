---
type: Uni Note
class:
  - "[[Calcolo delle Probabilità (class)]]"
academic year: 2023/2024
related: 
completed: false
created: 2024-09-25T14:20
updated: 2024-09-25T15:10
---
>[!abstract] Index
>1. 

>[!abstract] Related
>- 

>[!danger] TLDR

---
## Probabilità 

oss: $30\% = 0.3 = \frac{30}{100}$ 

## Spazio Campionario

>[!note] Definition
>- insieme dei possibili esiti 
>- simbolo: $S$

>[!example] Example
>Esperimento: lancio dado
>$S = \{ 1,2,3,4,5,6 \}$ 
>
  
---
## Evento 

>[!note] Definition
>Un evento è descritto matematicamente da un sotto sotto insieme di $S$, più precisamente dall'insieme degli esiti che realizzano l'evento.

>[!example] Example
>Esperimento: lancio del dado
>
>L'evento esce un numero pari è descritto dall’insieme $\{ 2,4,6 \} \subset S$
>
>**oss:** famiglia degli eventi = famiglia dei sotto insiemi di $S$.

>[!warning] Eventi Incopatibili
>
>Due eventi $E, F \subset S$, si dicono incompatibili se $E\cap F = \emptyset$
>
>Ovvero si dicono incompatibili se non esistono Esiti comuni.

>[!warning] Evento Certo
>Un evento si dice certo se qualsiasi evento avviene l'esito è confermato.
>
>**Da rivedere**

>[!warning] Evento Complementare
>Li esiti che non realizzano ..
>
>$$
>E^{c} = S\setminus E
>$$
>
>**Esempio:** 
>- lancio il dato 
>- $E = \text{esce }n<2= \{ 1,2 \}$
>- $E^{c} = S\setminus E = \{ 3,4,5,6 \}$

>[!warning] Evento Impossibile
>L'evento impossibile è descritto matematicamente da $\emptyset$
>
>Esempio: Se lancio un dato l'evento esce un numero negativo è impossibile.

## Spazio di probabilità

uno spazio di probabili tà è descritto dalla coppia $(S,P)$ dove:
- $S$ è lo spazio campionario dell'esperimento in considerazione
- P è la **funzione di probabilità** 


## Funzione di probabilità

è una funzione definita sulla famiglia degli eventi che soddisfano i seguenti assiomi:

>[!note] Assioma 1
>$$
>P(E) \in [0,1] \ \ \ \forall E \in S 
>$$

>[!note] Assioma 2
>$$
> P(S) = 1
>$$

>[!note] Assioma 3
>Data una successione $E_{1},E_{2}, \dots$ di eventi a 2 a 2 disgiunti vale:
>$$
>P\big(U^{\infty }_{i=1}E_{i} \big) = \sum^{\infty }_{i=1} P(E_{i})
>$$



oss: dato un evento $E$, $P(E)$ è detta probabilità dell'evento $E$