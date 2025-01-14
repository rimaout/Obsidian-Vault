---
type: Uni Note
class: "[[Basi di Dati 1 (class)]]"
academic year: 2024/2025
related: 
completed: false
created: 2024-12-12T13:21
updated: 2024-12-20T21:53
---
>[!abstract] Related
>- 

---
## Introduzione

Quando le chiavi ammettono un ordine, è più conveniente utilizzare un organizzazione fisica che tenga conto di questa caratteristica dei dati.

>[!note] Ordinamenti
>La maggior parte dei data type hanno un ordinamento
>- Valori numerici per confronto
>- Stringhe ordine lessicografico
>
>Se abbiamo dati composti da campi multipli, si ordina il primo campo, poi il secondo e cosi via (oss: l'ordinamento lessicografo si comporta allo stesso modo in cui i vari simboli rappresentano i campi)
>
>>[!warning]- Algoritmo di Ordinamento
>>
>>Le condizioni appena viste sono equivalenti al seguente algoritmo:
>>- Si pone n=1
>>- Si confrontano i simboli nella posizione n-esima della stringa:
>>    - Se una delle due non possiede l’elemento n-esimo allora è minore dell’altra e terminiamo
>>    - Se entrambe le stringhe non possiedono l’elemento n-esimo allora sono uguali e l’algoritmo termina
>>    - Se i simboli sono uguali si passa alla posizione successiva
>>    - Se questi sono diversi, il loro ordine è l’ordine delle stringhe

---
## File con Indice Sparso

Un esempio di file and indice sparso può essere un file **ISAM** (Indexed Sequential Access Method)

Questa struttura è composta da due file: 

>[!note] File Principale
>
>Questo file è ordinato in base alle chiave dalla più piccola alla più grande ed i record sono distribuiti sugli blocchi. 
>
>Solitamente lasciando un po’ di spazio libero in ogni blocco, per permettere di inserire nuovi elementi in futuro.

>[!note] File Indice
>
>Il file indice contiene un record per ogni blocco del file principale.
>
>I record sono composti da due campi:
>1. un *puntatore ad blocco* del file indice
>2. il più piccolo valore della *chiave* presente nel blocco
>   
>Anche questi record sono ordinati dal più piccolo al più grand, utilizzando come valore di ordinamento la *chiave*.
>
>![[Pasted image 20241220150200.png|450]]
>
>***oss:*** $-\infty$ è una convenzione per indicare il puntatore al primo blocco. 

---
## Ricerca

Per ricavare un record con valore della chiave `k` occorre ricercare sul file indice un valore `k'` della chiave che ricopre `k`, cioè tale che:
- `k <= k''
- se il record con chiave `k'` non è l’ultimo record del file indice e `k''` è il valore della chiave nel record successivo `k < k''`.
  
Una volta scelto il *record del file indice* utilizziamo il suo puntatore per andare a cercare il record nel blocco del file principale.

La ricerca di un record con chiave `k` richiede una [[#Ricerca su file indice]] più un accesso in lettura sul file principale.

>[!warning] Ovvero
>Per cercare in un file indice che corrisponda a una chiave specifica `k`. Per far ciò, devi cercare un record nel file indice che abbia una chiave `k'` che sia la più vicina possibile a `k`, ma non superiore.
>
>In altre parole, devi trovare il record con la chiave più grande che sia minore o uguale a `k`. 

>[!example]- Esempio
>
>![[Pasted image 20241220150200.png|450]]
>
>Ad esempio il record con chiave 090 deve trovarsi nel blocco del file principale che contiene 031 come valore più piccolo, dato che nel precedente il valore più piccolo è 003 e nei successivi sono $>=$ 101.
>
>Oppure il record con chiave 234 deve trovarsi nell’ultimo blocco del file principale dato che nei precedenti i valori della chiave sono < 220.

#### Ricerca su file indice

>[!note] Ricerca Binaria
>
>Dato che il file indice è ordinato in base al valore della chiave, la ricerca di un valore che ricopre la chiave può essere effettuata tramite la ricerca binaria:
>
>- Si fa un accesso in lettura al blocco $\frac{n}{2}+1$ e si confronta `k` con `k1` (prima chiave del blocco)
>- Se `k = k1` abbiamo finito
>- Se `k < k1` allora si ripete il procedimento sui blocchi da $1$ a $\frac{n}{2}$​
>- Altrimenti si ripete il procedimento sui blocchi da $\frac{n}{2}+1$​ a $n$ (ricontrolliamo anche questo blocco dato che prima abbiamo controllato solo la prima chiave e non il resto del blocco)
>
>Ci si ferma quando lo spazio di ricerca è ridotto ad un unico blocco e quindi dopo ⌈log2​m⌉ accessi

>[!note] Ricerca per Interpolazione
>

---
## Inserimento

Quando inseriamo ma il blocchi sono piene, non possiamo effettuare operazioni per spostare (ri-organizzare) i blocchi in 
sadff

![[Pasted image 20241212135747.png|500]]

Blocco giallo in questo esempio è detto lista di overflow

## Indice denso

Supponiamo di definire più indice su lo stesso file. Ovvero creare un indice sulla chiave primaria e uno su una chiave secondaria.

Problema i due indici devono avere lo stesso ordine, 

## Esempio 1 

**oss:** in questo caso c'è scritto che ogni blocco deve essere pieno all 70%, in particolare qui quai è **al più** al 70% questo vuol dire che se calcoliamo la grandezza dei blocchi da utilizzare possiamo prendere la parte intera inferiore) al meno prendiamo la parte intera superiore.