---
type: Uni Note
class:
  - "[[Basi di Dati 1 (class)]]"
academic year: 2023/2024
related: 
completed: false
created: 2024-09-26T13:09
updated: 2024-10-10T12:46
---
>[!abstract] Index
>1. 

>[!abstract] Related
>- 

---
## Modella relazionale 

Questo tecnica è stata introdotta nel 1970, ed ha permesso l'indipendenza dei dati.

>[!warning] Indipendenza
>Con indipendenza si intende ...
>

>[!note] Funzionamento
>- Basato dulla nozione matematca di relazione 
>- Le relazioni si traducono in tabelle (tabella e ralzione si usano come termini intercambiabili)
>- dati e relazioni 

>[!warning] 3 tipi di relazione
>- **Relazione matematica:**
>- **Relazione:**
>- **Entity relationship:**

## Definizioni utili

>[!note] Dominio
>Un insieme possibilmente infinito di valori.
>
>**Esempi:**
>- l’insieme dei numeri interi è un dominio
>- l’insieme dei numeri decimali è un dominio
>- l’insieme delle stringhe di caratteri di lunghezza = 20 è un dominio
>- {0,1} è un dominio
d

>[!note] Relazione Matematica
>Una relazione matematica è un qualsiasi sottoinsieme del prodotto Cartesiano di uno o più domini.
>
>
>- Una relazione che è sottoinsieme del prodotto Cartesiano di k domini si dice di grado k.
>- Gli elementi della relazione sono detti **Tuple**.
>- Il numero di tuple di una relazione è la sua **Cardinalità**.
>- Il numero di attributi ........... è detto **Grado**.
>- Il numero di domini di una relazione è detto **Grado**.


![[Pasted image 20240926132959.png|500]]


>[!note] Schema di base di dati
>è un insieme di schemi di relazione con nomi differenti.

---
## Integrità dei Valori

Vincolo di integrità: proprietà che deve essere soddisfatta da ogni istanza della base di dati (legata quindi allo schema)

- I vincoli descrivono proprietà specifiche del campo di applicazione, e quindi delle informazioni ad esso relative modellate attraverso la base di dati

- Una istanza di base di dati è corretta se soddisfa tutti i vincoli di integrità associati al suo schema

![[Pasted image 20240926134958.png|500]]

>[!note] Vincoli Intra-Relazionali
>Vincoli intra-relazionali: definiti sui valori di singoli attributi (di dominio) o tra valori di attributi di una stessa tupla o tra tuple della stessa relazione
>
>>**Esempio:** Valore lode può essere vero solo de il voto è 30.

>[!note] Vincoli Inter-Relazionali

>[!note] Vincoli di dominio
>

>[!note] Vincoli di tupla


**Vincolo di integrità referenziale (foreign key):** porzioni di informazione in relazioni diverse sono correlate attraverso valori di chiave.


>[!note] Istanza Legale
>Istanza Legale è un instanza sel sistema che risetta tutte le dipendenze fondamentali.

## Dipendenze Funzionali 

Una dipendenza funzionale stabilisce un particolare legame semantico tra due insiemi non-vuoti di attributi X e Y appartenenti ad uno schema R

>[!tip] Simbologia
>- Tale vincolo si scrive $X\to$ Y e si legge $X$ determina $Y$.
>- Quando si utilizzano le prime letter dell'alfabeto $a, b, c ...$$ si indicano i singoli elementi.
>- Quando si usano i simboli $X, Y, Z$ si indicano insiemi di attribbuti.

>[!warning] Esempio
>Supponiamo di avere uno schema di relazione: 
>$$
>\text{VOLI (CodiceVolo, Giorno, Pilota, Ora)}
>$$
>
>Degli esempi di vincoli sono:
>1. Un volo con un certo codice parte sempre alla stessa ora
>2. Esiste un solo volo con un dato pilota, in un dato giorno ad una data ora
>3. C’è un solo pilota di un dato volo in un dato giorno.
>
>I vincoli corrispondono alle dipendenze funzionali:
>1. CodiceVolo → Ora
>2. {Giorno, Pilota, Ora} → CodiceVolo
>3. {CodiceVolo, Giorno} → Pilota
>
>>**oss:** non sarebbe possibile: CodiceVolo -> {Giorno, Pilota, Ora}, stesso codice volo può essere utilizzato per indicare lo stesso volo che avviene in giorni diversi.

>[!note] Soddisfare Dipendenza Funzionale
>Diremo che una relazione $r$ con schema $R$ **soddisfa** la dipendenza funzionale $X \to Y$ se:
>1. La dipendenza funzionale $X \to Y$ è applicabile ad R, nel senso che sia $X$ sia il $Y$ sono sottoinsiemi di $R$;
>2. Le n-nuple in $r$ che concordano su $X$ concordanoanche su $Y$, cioè per ogni coppia di n-tuple $t_{1}$ e $t_{2}$ in $r$ $t_{1}[X] = t_{2}[X] \implies t_{1}[Y] = t_{2}[Y]$.

---
