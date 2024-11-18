---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2024-11-17T18:40
updated: 2024-11-17T18:55
---
>[!abstract] Related
>- 

---
## Introduzione

La [[Memoria Virtuale|paginazione con memoria virtuale]] è il metodo principale con cui i sistemi operativi moderni gestiscono la memoria, però prima dobbiamo vedere come funzione una paginazione senza memoria virtuale anche detta [[#Paginazione Semplice|paginazione semplice]].

---
## Paginazione Semplice

La memoria viene partizionata in pezzi di grandezza uguale e piccola, stesso trattamento avviene per i processi.
- i *pezzi di processi* sono chiamati **pagine**
- i *pezzi di memoria* sono chiamati **frame**

>[!note] Pagine e Frames
>Ogni pagina, per essere usata, dev’essere collocata in un frame, ma non è importante in quale frame viene inserita, infatti:
>- pagine che appartengono allo stesso possono anche essere in posizioni distanti
>- una pagina ed un frame hanno la stessa dimensione

