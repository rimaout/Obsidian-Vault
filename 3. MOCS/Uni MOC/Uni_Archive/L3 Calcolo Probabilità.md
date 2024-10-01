---
type: Uni Note
class:
  - "[[Calcolo delle Probabilità (class)]]"
academic year: 2023/2024
related: 
completed: false
created: 2024-09-25T14:20
updated: 2024-10-01T13:43
---
>[!abstract] Index
>1. 

>[!abstract] Related
>- 

---
## Probabilità 

oss: $30\% = 0.3 = \frac{30}{100}$ 

  
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

---
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

>[!note] Assioma 3 (additiva numerabile)
>Data una successione $E_{1},E_{2}, \dots$ di eventi a 2 a 2 disgiunti (incompatibili) vale:
>$$
>P\big(U^{\infty }_{i=1}E_{i} \big) = \sum^{\infty }_{i=1} P(E_{i})
>$$

oss: incompatibilità tra eventi: $\forall  i = j \exists:E_{i} \cap j \not = 0$

oss: dato un evento $E$, $P(E)$ è detta probabilità dell'evento $E$

>[!danger] Prop
>$$
>P(\emptyset) = 0
>$$
>
>**Dim:**
>Prendo la successione $E_{1}, E_{2}, \dots$ dove
>- $E_{1} = \emptyset, E_{2} = \emptyset, E_{3} = \emptyset$ 
>
>cnskjnkjdz
>se fosse $P(\emptyset) \in (0,5] avrei \sum^{\infty}_{i=1}P(\emptyset) = +\infty$
>e quindi $P(\emptyset) \not = \sum^{\infty}_{i=1}P(\emptyset)$
>
>Per esclusione deve essere $P(\emptyset) = 0$

>[!danger] Prop
>$P$ soddisfa l’aditività  finita
>
>dati $n$ eventi a 2 a2 incompatibili $E_{1}, E_{2}, \dots, E_{n}$
>
>$P\big(U^{\infty }_{i=1}E_{i} \big) = \sum^{u}_{i=1}$
>
>**Dim:**
>consideriamo la successione $F_{1}, F_{2}, \dots$ con: 
>$$
>F_{1} = E_{1}, F_{2} = E_{2}, \dots , F_{n}=E_{n}, F_{n+1} = \emptyset, F_{n+1} = \emptyset 
>$$
>Questa è una bella successione l.cnzkljsvnljkznvslkzjnajks<
>
>Ho che $P\big(U^{\infty }_{i=1}E_{i} \big) = \sum^{u}_{i=1}$
>lsdjv<k<vk.zvnjklxn

>[!danger] Prop
>Consideriamo un evento $E$ la probabilità del suo evento complementare $E^{c}$ sarà:
>$$
>P(E^{c}) = 1 - P(E)
>$$
>
>>[!warning]- Dim
>>$E$ ed $E^{c}$ sono eventi incompatibili kdkljshdkjladhjkhjkh

>[!danger] Prop
> Dati due eventi $F$ ed $E$ con $E \subset F$  vale che:
>$$
>P(F) \leq P(E)
>$$
>
>>[!warning]- Dim
>>![[Pasted image 20240930182639.png|400]]

>[!danger] Prop
>Somma della probabilità di eventi non disgiunti (non incompatibili)
>$\forall E,F$ eventi $P(E\cup F) = P(E) + P(F) - P(E\cap F)$



---
