---
type: Uni Note
class: 
academic year: 2023/2024
related: 
completed: false
created: 2024-09-26T13:09
updated: 2024-09-28T19:50
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

>[!note] Prodotto cartesiano
> Siano $D_{1}, D_{2}, \dots, D_{k}$
>
>Il prodotto cartesiano $D_{1} \times D_{2} \times \dots \times D_{k}$
>
>é l'insieme 
>$$
>\{ (v_{1}, v_{2}, \dots v_{k}): dacontinuare\dots\dots. \}
>$$



>[!note] Relazione Matematica
>Una relazione matematica è un qualsiasi sottoinsieme del prodotto Cartesiano di uno o più domini.
>
>
>- Una relazione che è sottoinsieme del prodotto Cartesiano di k domini si dice di grado k.
>- Gli elementi della relazione sono detti **Tuple**.
>- Il numero di tuple di una relazione è la sua **Cardinalità**.
>- Il numero di attributi ........... è detto **Grado**.
>- Il numero di domini di una relazione è detto **Grado**.

**Esempio di relazione con due 4-ple su String, String, Integer, Real:**

| Nome  | Cognome | Esami Sostenuti | Media |
| ----- | ------- | --------------- | ----- |
| Paolo | Rossi   | 2               | 26.5  |
| Mario | Bianchi | 10              | 28,7  |

![[Pasted image 20240926132959.png|500]]


>[!note] Attributo
>Un attributo è definito da un **Nome** $A$ e dal **Dominio** dell'attributo $A$ che dichiamo con $dom(A)$

![[Pasted image 20240926133426.png|500]]

## Rappresentazione di una relazione

Una relazione può essere implementata come una tabella in cui ogni riga è una tupla della relazione differente da ogni altra e ogni colonna corrisponde ad una componente (valori omogenei, cioè provenienti dallo stesso dominio)

Le colonne corrispondono ai domini D1,D2,.....Dk e hanno associati dei nomi univoci all’interno della tabella, detti nomi degli attributi (descrivono il ruolo)

La coppia (nome di attributo, dominio) è chiamata attributo. L’insieme di attributi di una relazione è detto schema

Se una relazione è denominata $R$ e i suoi attributo hanno nomi $A_{1}, A_{2},.....,A_{k}$, lo schema è spesso indicato da $R(A_{1}, A_{2},.....,A_{k})$

>[!note] Schema 
>Uno schema di relazione 

>[!note] Istanza 
>Un instanza di relazione 

>[!note] Schema di base di dati
>è un insieme di schemi di relazione con nomi differenti.

**Esempio schema e istanza:**
![[Pasted image 20240926133944.png|500]]

---

## Valori Nulli

>[!note] Definizione
>I valori nulli rappresetano la mancanza di un informazione o il fatto che l'informazione non è reperibile.

>[!warning] Esempio
>Numero di telefono:
>- la persona non ha il telefono
>- non so se la persona ha il telefono
>- la persona ha il telefono ma non ne conosco il numero

>[!danger] Not NULL
>Alcuni campi NON DOVREBBERO MAI assumere valori
>
>**Esempio:** Matricola di uno studente 

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

---
## Chiavi

Una chiave di una relazione (non è detto che sia unica) è un attributo o insieme di attributi che identifica univocamente una tupla.

Le chiavi di uno schema si definiscono con le dipendenze funzionali.

Un insieme di attributi che continenti una chiave è detto **super chiave**.

Un insieme X di attributi di una relazione R è una chiave di R se soddisfa le seguenti condizioni:

1. Per ogni istanza di R, non esistono due tuple distinte t1 e t2 che hanno gli stessi valori per tutti gli attributi in X, tali cioè che t1[X] = t2[X]

2. Nessun sottoinsieme proprio di X soddisfa la condizione 1)


>[!warning] Chiavi Alternative
>Una relazione potrebbe avere più chiavi una primaria e delle chiavi alternative.
>- Si sceglie quella più usata o quella composta da un numero minore di attributi = chiave primaria
>
>
>>**oss:** La chiave primaria non ammette valori nulli

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

![[Recording 20240926150358.webm]]


---
---
---
## Parte 2 (Algebra Relazionale)

>[!note] Linguaggio Formale
>L'algebra relazionale è un operatore formale (nel senso che non esiste un linguaggio eseguibile).

>[!note] Linguaggio Procedurale


## Operatori


#### Proiezione

>[!note] Definizione
>Consente di effettuare un “taglio verticale” su una relazione, cioè di selezionare solo alcune colonne (attributi)

>[!note] Simbologia
>$$
>\pi A_{1}, A_{2}, \dots , A_{k} (r)
>$$

>[!example] Esempio
>![[Pasted image 20240926153930.png|400]]
>
>**Query:** Nomi dei clienti, ovvero:
>$$
>\pi_{\text{nome}}(\text{CLIENTE})
>$$
>**Output:**
>![[Pasted image 20240926154114.png|120]]
>
>>**oss:** I doppioni vengono tagliati
>>Se vogliamo conservare i clienti omonimi dobbiamo aggiungere un ulteriore attributo, in questo caso la (una) «chiave» (il codice)

---
#### Selezione

>[!note] Simbologia
>$$
>\sigma_{C} \big( r \big)
>$$

kavhkbkaszkvbzksbvkz


---
#### Unione

 

---
