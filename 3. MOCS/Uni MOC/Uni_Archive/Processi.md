---
type: Uni Note
class:
  - "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related: 
completed: false
created: 2024-10-04T18:51
updated: 2024-10-04T19:54
---
>[!abstract] Index
>1. 

>[!abstract] Related
>- [[Sistemi Operativi 1 (class)]]

---
## Introduzione

Uno dei compiti principali dei sistemi operativi è la **gestione dei processi**, in particolare un sistema operativo deve permettere:
- Esecuzione alternata di processi multipli (**interleaving**).
- Assegnare le risorse ai processi, e proteggere dagli altri processi.
- Scambio di informazioni tra processi.
- Sincronizzazione dei Processi.

>[!note] Definizione di Processo
>Si tratta di un'istanza di un programma in esecuzione, ed è composto da:
>- Codice (anche condiviso).
>- Un insieme di dati.
>- Attribbuti che descrivono lo stato del processo.

---
## Fasi

Un processo ha tre fasi creazione, esecuzione e terminazione.

>[!warning] Terminazione
>Ci sono due tipi di terminazioni:
>
>1. La **Terminazione Prevista:** che può avvenire perché il processo ha terminato il suo scopo e si "chiude" in automatico, o voluta dall'utente che "chiude" in modo controllato il processo. 
>2. La **Terminazione NON Prevista:** che può avvenire per l’esecuzione di un istruzione non consentita, che richiede l'intervento del sistema operativo per la "chiusura" forzata del processo.
>   
>>**oss:** Esistono anche processi che rimangono sempre in esecuzione.

---
## Elementi

Finche un processo è in esecuzione, ad esso sono associate delle informazioni, tra le quali:
- Identificatore (per distinguerlo da altri processi)
- Stato (running... )
- Priorità 
- Hardware Context (valore corrente dei registi della CPU, compreso program counter)
- Puntatori a Memoria (immagine del processo)
- Stato dell'I/O
- Informazioni di accounting (utente che sta eseguendo il processo)

>[!note] Process Control Block
>
>>[!column|flex]
>>
>>>[!note|clean no-t]
>>>Insieme di informazioni create dal sistema operativo per ogni processo che:
>>>- Salvate nella zona riservata al [[Kernel]] (accessibile soltanto all'OS).
>>>- Contiene gli [[#Elementi]] del processo.
>>>- Permette la gestione di più processi, ovvero contiene sufficienti informazioni per bloccare un programma in esecuzione e farlo riprendere più tardi dallo stesso punto in cui si trovava.
>>
>>>[!caption|right]
>>> 
>>>![[Pasted image 20241004194346.png|120]]

