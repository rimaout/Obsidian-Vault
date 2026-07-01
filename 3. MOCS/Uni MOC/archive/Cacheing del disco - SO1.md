---
type: Uni Note
class:
  - "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2026-02-04T14:35
updated: 2026-06-27T17:16
---
## Introduzione

Come abbiamo visto nella sezione [[Cache]], le cache (della RAM) sono delle memorie molto veloci posizionate all'interno dei processori, che vengono utilizzare per ridurre e velocizzare le letture in memoria RAM.

Adesso però parleremo della cache del disco anche detta **Page Cache**, ovvero un buffer in memoria principale (RAM) che contiene una copia di alcuni settori del disco. Quando si fa una richiesta di I/O per dati che si trovano su un certo settore, si vede prima se tale settore è nella cache

>[!warning] 
>
>La page cache non va confusa con la cache spesso presente direttamente sui dischi.

Ci sono svariati metodi per gestire questa cache, in particolare le politiche di ripianamento:
- [[#LRU - Least Recently Used]]
- [[#LFU - Least Frequently Used]]
- [[#FBR - Frequency Based Replacement]]
## LRU - Least Recently Used

Se occorre inserire un settore nella cache, ed è piena, si rimpiazza quello che è da più tempo nella cache senza accesi.

**Struttura:** La cache viene puntata da uno *“stack”* di puntatori, dove in cima è presente il puntatore al settore usato più di recente. Quindi ogni volta che un settore viene referenziato o copiato nella cache, il suo puntatore viene portato in cima allo stack

## LFU - Least Frequently Used

Se la cache è piena e occorre inserire un nuovo settore, l'algoritmo *sostituisce il settore che ha registrato il minor numero di accessi* (frequenza più bassa).

Ogni settore presente nella cache è associato a un contatore dedicato:
- **Inizializzazione:** Quando un settore viene inserito in cache, il suo contatore viene impostato a `1`.
- **Aggiornamento:** A ogni successivo accesso a quel determinato settore, il rispettivo contatore viene incrementato di `1`.

**Limiti** - Sebbene la logica di LFU possa sembrare più intuitiva rispetto a quella di LRU (_Least Recently Used_), l'algoritmo presenta un limite strutturale legato al **principio di località temporale**:
- Un settore può essere richiesto moltissime volte di fila in un breve lasso di tempo (ad esempio, all'interno di un ciclo). Questo fa impennare il valore del suo contatore.
- Una volta terminata quella specifica fase del programma, il settore **non serve più**, ma il suo contatore ha ormai raggiunto un valore molto alto. Di conseguenza, il settore rimarrà bloccato in cache a lungo, occupando spazio inutilmente, poiché l'algoritmo tenderà a non sostituirlo.

## FBR - Frequency Based Replacement

Approccio ibrido tra [[#LRU - Least Recently Used|LRU]]  e [[#LFU - Least Frequently Used|LFU]], l'obiettivo è evitare che la cache venga "inquinata" da blocchi che vengono letti moltissime volte in un brevissimo lasso di tempo e poi mai più usati (limite del LFU).

>[!note] Idea Iniziale - Divisione in 2 parti (Nuova e Vecchia)
>
>La struttura nasce dalla combinazione di:
>- puntatori a blocchi sotto forma di **stack**, come in [[#LRU - Least Recently Used|LRU]]
>- ogni blocco ha anche un **contatore degli accessi**, come in [[#LFU - Least Frequently Used|LFU]]
>
>Dove lo stack viene diviso in due zone (Nuova e Vecchia), con regole diverse:
>- Quando un nuovo blocco viene caricato, è inserito in cima alla parte **Nuova** e il suo contatore viene impostato a `1`
>- Quando viene effettuato un **accesso** ad un blocco che si trova nella **parte nuova**, viene spostato in cima alla parte nuova, ma il suo *contatore NON viene incrementato*
>- Quando viene effettuato un **accesso** ad un blocco che si trova nella **parte Vecchia**, viene spostato in *cima alla parte nuova* e il suo *contatore viene incrementato*
>- **Rimpiazzo (Cache Piena):** Quando dobbiamo fare spazio a un nuovo blocco, guardiamo solo nella parte Vecchia ed eliminiamo il blocco con il **contatore minimo**.
>  
>>[!warning] Limiti
>>
>>Quando un blocco con contatore di frequenza uguale a 1, passa dalla parte "nuova" alla parte "vecchia", ha un altissima probabilità di venir rimosso prima di poter incrementare il contatore (a due), invece quando un blocco riesce ad arrivare ad un contatore `>=` 2 diventa molto difficile rimoverlo.

>[!note] Versione Finale - Divisione in 3 Segmenti
>
>- ***Nuovo***: i contatori non vengono incrementati, non effettuiamo rimpiazzi qua dentro
>- ***Medio***: I contatori vengono incrementati ma non possiamo comunque fare rimpiazzi
>- ***Vecchio***: Contatori incrementati e rimpiazzi possibili
