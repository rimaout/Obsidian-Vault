---
created: 2024-04-12
type: Uni Note
class: 
academic year: 2023/2024
related: 
completed: false
updated: 2024-06-28T00:26
---
---

>[!info] Page Index
>1. 

---
## Progettazione di una CPU

-  Una CPU è un [[Circuiti sequenziali|circuito sequenziale]] (ovvero stato + [[Circuiti combinatori|circuito combinatorio]])


## Prima fase
**CPU MIPS Semplice e non ottimizzata:**
1. Definire come viene elaborata una istruzione ([[#Fasi di esecuzione]])
2. Scegliere [[#Istruzioni da realizzare]]
3. Scegliere le [[#Unità funzionali necessarie]]
4. Collegare le unità funzionali
5. Costruire la CU (Contro Unit) che controlla il funzionamento della CPU
6. Calcolare il massimo tempo di esecuzione delle istruzioni (periodo di clock)

---
##### Fasi di esecuzione 
| Istruzione                            | Info                                                        |
| ------------------------------------- | ----------------------------------------------------------- |
| Fetch                                 | Caricamento di un istruzione dalla memoria alla CU          |
| Decodifica                            | Decodifica dell'istruzione e lettura argomenti dei registri |
| Esecuzione                            | attivazione delle unità funzionali necessarie               |
| Memoria                               | accesso alla memeria                                        |
| Write Back                            | scrittura dei risultati nei registri                        |
| Aggiornamento de PC (Program Counter) | normale / salti condizionati / salti non condizionati       |
 
>[!warning] Parallelismo interno
>Posso eseguire alcune operazione in parallelo
>- Esempio: eseguire una somma algebrica e allo stesso tempo decodificare un istruzione

---
##### Istruzioni da realizzare


| Instruzione                     | Info                          | Tipo |
| ------------------------------- | ----------------------------- | ---- |
| `lw`, `sw`                      | accesso alla memoria          | I    |
| `beq`                           | salti condizionati            | I    |
| `add`, `sub`, `sli`, `slt`, ... | operazione aritmetico-logiche | R    |
| `j`, `jal`                      | salti non condizionati        | J    |
| `li`, `add`, `subi`, ...        | operazioni con cosati         | I    |

![[Pasted image 20240412115752.png|900]]

---
##### Unità funzionali necessarie

| Unità funionale    | info                                              |
| ------------------ | ------------------------------------------------- |
| PC                 | registro che contiene l'indirizzo dell'istruzione |
| memoria istruzione | contiene le istruzioni                            |
| adder              | per calcolare valori PC (successivo o salto)      |
| registri           | contengono gli argomenti delle istruzioni         |
| ALU                | fa operazioni aritmetico logiche                  |
| memoria dati       | da cui leggere e scrivere i dati (load/store)     |
###### Memoria delle Istruzioni


###### PC


###### Adder


###### ALU

![[Pasted image 20240412124829.png|250]]

- Riceve due valori interi a 32 bit e svolge una operazione indicata dai segnali Op. ALU
- Oltre al risultato da 32 bit produce un segnale «Zero» asserito se il risultato è zero

###### Registri

![[Pasted image 20240412124945.png|400]]

- contiene 32 registri a 32 bit, indirizzabili con 5 bit (2^5 = 32)
- può memorizzare un dato in un registro e contemporaneamente fornirlo in uscita
- 3 porte a 5 bit per indicare quali 2 registri leggere e quale registro scrivere
- 3 porte dati (a 32 bit)
	- una in ingresso per il valore da memorizzare e
	- 2 di uscita per i valori letti
- il segnale RegWrite abilita (se 1) la scrittura nel registro di scrittura

###### Memoria Dati 

###### Unità estensione segno

---
## Fetch delle Istruzione/aggiornamento del PC

![[Pasted image 20240412125253.png|800]]

---

