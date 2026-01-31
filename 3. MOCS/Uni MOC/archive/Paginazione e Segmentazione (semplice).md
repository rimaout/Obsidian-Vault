---
type: Uni Note
class: "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related:
completed: false
created: 2024-11-17T18:40
updated: 2026-01-31T13:32
---
>[!abstract] Related
>- 

---
## Introduzione

La paginazione - e a volte la segmentazione -  con [[Memoria Virtuale|memoria virtuale]] è il metodo principale con cui i sistemi operativi moderni gestiscono la memoria, però prima dobbiamo vedere come funzionano la paginazione e segmentazione senza memoria virtuale, anche dette semplici:
- [[#Paginazione Semplice]]
- [[#Segmentazione Semplice]]

---
## Paginazione Semplice

La memoria e processi vengono partizionati in pezzi di grandezza uguale e piccola.
- i *pezzi di processi* sono chiamati ***pagine***
- i *pezzi di memoria* sono chiamati ***frame***

>[!note] Pagine e Frames
>Ogni pagina, per essere usata, dev’essere collocata in un frame, ma non è importante in quale frame viene inserita, infatti:
>- pagine che appartengono allo stesso possono anche essere in posizioni distanti
>- una pagina ed un frame hanno la stessa dimensione

aiuto hardware

>[!note] Tabella delle Pagine
>Il sistema Operativo per ogni Processo mantiene una tabella delle pagine.
>- Per ogni pagina del processo, questa tabella dice in quale frame effettivo si trova
>- Quando c’è un `process switch`, la tabella delle pagine del nuovo processo deve essere ricaricata
>  
>Questo lavoro richiede un grande overhead ma è totalmente giustificato dalla semplicità di gestione della memoria che si ottiene.

>[!example] Esempio
>![[3. MOCS/Uni MOC/archive/attachments/jkhv34254tvkadwlkh3.png]]
>
>**Tabelle delle pagine risultanti:**
>
>![[3. MOCS/Uni MOC/archive/attachments/Pasted image 20241122121029.png|600]]

---
## Segmentazione Semplice

I *programmi* possono essere *divisi in segmenti*, segmenti che possono avere una lunghezza variabile ma la dimensione massima è limitata.

>**oss:** un indirizzo di memoria è rappresentabile attraverso il numero di un segmento e una spaiamento al suo interno.

Il funzionamento è simile al [[Partizionamento#Partizionamento Dinamico|partizionamento dinamico]], ma con una ***differenza fondamentale*** è *programmatore (o compilatore) gestisce la segmentazione*:
- programmatore decide la quantità e dimensione dei segmenti
- il caricamento in RAM e la risoluzione degli indirizzi viene effettuata dal OS.

>[!note] Tabella dei segmenti
>Il sistema Operativo per ogni Processo mantiene una tabella delle pagine dove ogni segmento del processo è associato con un indirizzo in memoria.

>[!example] Esempio accesso indirizzo si memoria
>
>Questo esempio ci mostra in usando tre metodi diversi come si accede alla memoria
>
>![[3. MOCS/Uni MOC/archive/attachments/Screenshot 2024-11-23 at 11.26.16.png|900]]
>
>**Primo caso (a) riguarda gli [[Gestione della Memoria (introduzione)#^cc500d|indirizzi relativi]]:**
>- Per andare ad un determinato indirizzo dobbiamo sapere dove comincia il processo, e sommare il suo indirizzo iniziale (base) a quello dell’istruzione (relativo).
>
>**Secondo caso (b) riguarda la [[#Paginazione Semplice]]:**
>- Per accedere a un determinato indirizzo, dobbiamo prima identificare la pagina in cui si trova.
>- Una volta che abbiamo la pagina possiamo utilizzare la tabella delle pagine per scoprire in che frame di memoria si trova. 
>- Una volta che abbiamo il frame ci basta sommare lo spiazzamento per raggiungere il giusto indirizzo di memoria.
>  
>**Terzo caso  (c) riguarda la [[#Segmentazione Semplice]]:**
>- Funzionamento analogo alla paginazione ma abbiamo una tabella dei segmenti invece della tabella delle pagine ed ogni segmento può avere una lunghezza diversa.

