---
type: Uni Note
class: "[[Basi di Dati 1 (class)]]"
academic year: 2024/2025
related:
  - "[[Introduzione all'organizzazioni dei database]]"
completed: true
created: 2024-11-30T19:23
updated: 2025-01-30T18:48
---
>[!abstract] Related
>- [[Introduzione all'organizzazioni dei database]]
>- [[Basi di Dati 1 (class)]]

---
## Introduzione

In questo tipo di file non c'è una vera e propria organizzazione dei record, i nuovi record vengono semplicemente inseriti come ultimo record del file.

>[!note] Accesso ai File
>L’accesso al file avviene attraverso una directory che contiene i puntatori ai blocchi, se le dimensioni lo consentono (se la directory entra in un unico blocco), tale directory può essere mantenuta in memoria principale durante l’utilizzo del file; altrimenti saranno necessari ulteriori accessi per portare in memoria principale i necessari blocchi della directory.

>[!info] Pro / Contro
>Il fatto di non adottare nessun particolare accorgimento nell’inserimento dei record che possa poi facilitare la ricerca:
>- ci fornisce le prestazioni peggiori in termini di numero di accessi in memoria richiesti dalle operazioni di ricerca 
>- mentre l’inserimento è molto veloce se ammettiamo duplicati

>[!note] Operazioni
>- [[#Ricerca]]
>- [[#Inserimento]]
>- [[#Modifica]]
>- [[#Cancellazione]]

---
## Ricerca

Se vogliamo cercare un record specifico dobbiamo cercare in tutto il file, iniziando dal primo record fino ad incontrare quello desiderato, quindi il tempo di ricerca varia in base a dove si trova il record. Se il record che cerchiamo si trova nell’i-esimo blocco avremo i accessi in memoria e quindi *ha senso valutare il costo medio di ricerca*.

***I valori che si conoscono sono:***
- $N = \text{numero totale di record}$
- $\text{rec} = \text{grandezza record (byte)}$
- $B = \text{grandezza blocco (byte)}$

***Valori da calcolare:***
- $R = \text{record x blocco} = \frac{rec}{B}$
- $n = \text{numero totale di blocchi} = \frac{N}{R}$

>[!example] Esempio Pratico
>- $N=151$ 
>- Ogni record ha 30 byte
>- Ogni blocco contiene 65 byte
>- Ogni blocco ha un puntatore di 4 byte al prossimo blocco
>
>**Quanti record interi possiamo inserire in ogni blocco?** Dobbiamo eseguire:
>
>$$
>\frac{65-4}{30}
>$$
>
>Ovvero $65−4$ perché è la dimensione del blocco meno la dimensione del puntatore, poi dividiamo per 30 che è la dimensione di un record.
>
>Otteniamo $2.03$ come risultato, ovviamente in un blocco non possiamo inserire dei record “a cavallo” e quindi prendiamo la *parte intera inferiore*, questo significa che in un blocco possiamo inserire 2 record. Quel 0.03 di blocco non possiamo memorizzarlo in un nuovo blocco.
>
>**Quanti blocchi servono per memorizzare N record?** Calcoliamo:
>
>$$
>\frac{N}{\text{Record per blocco}} = \frac{151}{2} = 75.5
>$$
>
>In questo caso dato che stiamo considerando i blocchi necessari per memorizzare un record, non *arrotondiamo* con la *parte* inferiore ma bensì con la *superiore*, quindi per memorizzare 151 record con i dati visti prima abbiamo bisogno di 76 blocchi.
>
>Quindi quando effettuiamo una ricerca dobbiamo scorrere una lista di 76 blocchi, se abbiamo fortuna troviamo subito il blocco, ma potrebbe anche trovarsi in ultima posizione.
>
>>**Esempio rubato da** [@alessio](https://alem1105.github.io/Quartz/Secondo-Anno/Primo-Semestre/Basi-di-Dati/BD1---Organizzazione-Fisica#file-hash)

#### Costo Medio

Per ottenere il costo medio occorre sommare i costi per accedere ai singoli record e dividere tale somma per il numero dei record. Per ognuno degli $R$ record nell’`i-esimo` blocco sono necessari `i`accessi.

>[!note] Formula
>$$
>\text{Costo Medio} = \frac{n}{2}
>$$
>
>Dove: $n$ è il numero di blocchi

>[!warning] Dimostrazione
>
>![[Pasted image 20241204112034.png|700]]
>
>$$
>\text{Costi Medio} = \frac{\text{accessi}}{\text{num. blocchi}} =  \frac{R(1+2 + \dots+ n)}{N} = \frac{R}{N} \cdot  (1 + 2 + \dots + n) = \frac{1}{n} \cdot  \frac{n(n+1)}{2} \approx \frac{n}{2}
>$$
>
>>***Formule usate per le semplificazioni***
>>$$
>>\begin{align*}
>>&\ \ \ \ \ \ \  - \text{sappiamo che } \frac{N}{R} = n \text{ quindi } \frac{R}{N} = \frac{1}{n}\\
>>&\ \ \ \ \ \ \  - 1 + 2 + \dots + n = \sum_{1}^{n} k = \frac{n(n+1)}{2} \ \ \text{(Gauss)}
>>\end{align*}
>>$$

Se invece vogliamo cercare tutti i record con una determinata chiave che, in questo caso, **ammette duplicati** allora dovremmo accedere a tutti gli $n$ blocchi dato che non possiamo sapere quando abbiamo trovato l’ultima occorrenza.

---
## Inserimento 

Per effettuare l’inserimento abbiamo bisogno di 1 accesso in lettura per portare l’ultimo blocco in memoria principale e un altro accesso in scrittura per riscriverlo in memoria secondaria dopo averlo modificato. Questo accade se **ammettiamo duplicati**.

Se **non ammettiamo duplicati** l’inserimento è preceduto da una ricerca e quindi dobbiamo aggiungere una media di $\frac{n}{2}$​ accessi per verificare che non esista già un record con quella chiave.

---
## Modifica

Abbiamo come primo costo quello della ricerca, infatti dobbiamo trovare il record, poi dobbiamo aggiungere un accesso in scrittura per riscrivere il blocco in memoria una volta modificato, questo costo va ripetuto per ogni occorrenza della chiave, se ammettiamo duplicati.

---
## Cancellazione

Dobbiamo pagare il costo della ricerca. Se vogliamo evitare “buchi” dobbiamo pagare anche un accesso in lettura in più per leggere l’ultimo blocco e infine 2 accessi in scrittura, uno per riscrivere il blocco modificato e uno per riscrivere l’ultimo blocco dal quale abbiamo spostato l’ultimo record.
