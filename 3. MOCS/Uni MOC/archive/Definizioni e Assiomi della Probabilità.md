---
type: Uni Note
class:
  - "[[Calcolo delle Probabilità (class)]]"
academic year: 2024/2025
related: []
completed: true
created: 2024-10-01T12:25
updated: 2025-02-17T17:25
---
>[!abstract] Related
>- [[Calcolo delle Probabilità (class)]]

---
## Definizione di Probabilità


Una definizione semplice di probabilità è:

$$
P = \frac{\text{casi favorevoli}}{\text{casi possibili}}
$$

>[!danger] Inconveniente di questa definizione
>1. Funziona soltanto se tutti i casi possibili sono **Equi-Probabili**
>2. È una definizione **Circolare**. Questa definizione richiede che tutti i casi abbiano la stessa $\textcolor{orange}{\text{probabilità}}$ ma è proprio quello che stiamo provando a definire.
>3. Funziona soltanto se si utilizza un numero finito di casi.

---
## Spazio Campionario

>[!note] Definizione
>Lo **spazio campionario** rappresenta l'insieme di tutti possibili esiti di un esperimento,
>
>$$
>\text{Simbolo Matematico: S}
>$$

>[!example] Esempio
>Se l'esperimento è il lancio di un dado, lo spazio campionari di questo esperimento è:
>
>$$
>S = \{ 1,2,3,4,5,6 \}
>$$

---
## Evento

Un **evento** è descritto matematicamente da un sotto insieme di uno spazio campionario, in particolare rappresenta tutto gli esiti che realizzano l'evento.

>[!warning] Esempio
>**Esperimento:** Lancio del dado
>**Spazio Campionario:** $S = \{ 1,2,3,4,5,6 \}$
>
>L'evento "esce un numero pari" è descritto dall’insieme $\{ 2,4,6 \} \subset S$

>[!note] Probabilità di un evento
>La probabilità di un evento $E$ si rappresenta con $P(E)$ ed è un valore compreso tra 0 e 1, dove 0 indica che l'evento è impossibile e 1 che è certo.

##### Tipologie di Eventi

>[!note] Evento Certo
>
>Un evento è detto **certo** se contiene tutti gli elementi dello spazio campionario. In altre parole, un evento è certo se si verifica con certezza.
>
>$$
>\text{Evento certo: } A = S
>$$
>
>> [!warning] Esempio
>>  **Esperimento:** Lancio del dado 
>>  **Spazio Campionario:** $S=\{1,2,3,4,5,6 \}$$
>>
>> L'evento "esce un numero" è descritto dall’insieme $\{1,2,3,4,5,6\}$ es è uguale a $S$, quindi è un evento certo.

>[!note] Evento Impossibile
>
>Un evento è detto **impossibile** se è vuoto, ovvero non contiene alcun elemento dello spazio campionario. In altre parole, un evento è impossibile se non si verifica mai.
>
>$$
>\text{Evento impossibile: } A = \emptyset
>$$
>
>> [!warning] Esempio 
>> **Esperimento:** Lancio del dado 
>> **Spazio Campionario:** $S=\{1,2,3,4,5,6\}$
>> 
>> L'evento "esce un numero maggiore di 6" è descritto dall’insieme $\emptyset$, quindi è un evento impossibile.

>[!note] Evento Complementare
>
>Un evento $E^{c}$ è detto **complementare** di un altro evento $E$, se è l'insieme di tutti gli elementi dello spazio campionario che non sono in quell'evento.
>
>$$
>E^{c} = S \setminus E
>$$
>
>> [!warning] Esempio 
>> **Esperimento:** Lancio del dado 
>> **Spazio Campionario:** $S={1,2,3,4,5,6}$
>> 
>> L'evento "esce un numero pari" è descritto dall’insieme $E=\{2,4,6\}$. L'evento complementare di E è $E^c =\{1,3,5\}$.

>[!note] Evento Incompatibile
>
>Due eventi $E$ ed $F$ sono detti **incompatibili** se la loro intersezione è vuota. In altre parole, due eventi sono incompatibili se non possono verificarsi contemporaneamente.
>
>$$
>\text{Eventi incompatibili: } E \cap F = \emptyset
>$$
>
>> [!warning] Esempio 
>> **Esperimento:** Lancio del dado 
>> **Spazio Campionario:** $S=\{1,2,3,4,5,6\}$
>> 
>> L'evento "esce un numero pari" è descritto dall’insieme $\{2,4,6\}$ e l'evento "esce un numero dispari" è descritto dall’insieme $\{1,3,5\}$. Questi due eventi sono incompatibili.

^14f29a

---
## Spazio di Probabilità

Uno **spazio di probabilità** è descritto dalla coppia $(S, P)$ dove:
- $S$ è lo [[#Spazio Campionario|spazio campionario]] dell'esperimento in considerazione.
- P è la [[#Funzione di Probabilità|funzione di probabilità]]

---
## Funzione di Probabilità

La **funzione di probabilità** è una funzione definita sulla famiglia di eventi che soddisfa i seguenti tre assiomi:

>[!note] Assioma 1
>$$
>P(E) \in [0,1] \ \ \ \forall E \subset  S 
>$$

>[!note] Assioma 2
>$$
> P(S) = 1
>$$
>
>>**oss:** $P(S)$ è la probabilità che si ottenga un risultato qualsiasi che appartenga allo spazio campionario $S$

>[!note] Assioma 3 (additiva numerabile)
>Data una successione $E_{1},E_{2}, \dots$ di eventi a 2 a 2 disgiunti (incompatibili) vale:
>$$
>P \Big( \bigcup_{i=1}^{\infty}E_{i} \Big) = \sum_{i=1}^{\infty} P(E_{i})
>$$

^3a8a3d

