---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2026-02-16T09:45
updated: 2026-02-16T09:53
---
## Requisiti

**Particolarità:**
La struttura dei file può essere più flessibile, ovvero può avere delle variabili globali e delle funzioni ognuna con le proprie dichiarazioni di variabili. 

**Input:**
• -i, --in (notazione doppio trattino) per specificare il file di input
• -o --out (notazione doppio trattino) per specificare il file di output (***Opzionale***)
• -v, --verbose (notazione doppio trattino) per produrre o meno come output le statistiche di elaborazione (***Opzionale***)

**Statistiche:**
• numero di variabili controllate
• numero di errori rilevati
• per ogni errore rilevato, nome del file in cui e' stato rilevato e numero di riga nel file. 
• numero di righe di commento eliminate
• numero di file inclusi
• per il file di input la dimensione in byte ed il numero di righe (pre processamento)
• per ogni file incluso dimensione in byte e numero di righe (pre processamento)
• numero di righe e dimensione dell'output

(Opzionale ) ***fatto***: Restituire le statistiche di elaborazione sullo standard error invece che sullo standard output in modo da poter ridirezionare il file processato e le statistiche di elaborazione su due file diversi quando si seleziona la seconda modalità di output)

**Errori:**
L'applicazione sviluppata deve gestire i seguenti errori
• errore nei parametri di input, opzioni e relativi argomenti specificate da linea di comando
• errore di apertura dei file di input o specificati come argomento dell'include
• errore di chiusura file
• errore di lettura da file - ad esempio file vuoto o corrotto
• errore di scrittura su file

**Strutture dati:**
• Nella scelta delle strutture dati deve essere privilegiata l'allocazione dinamica della memoria
• In sede di esame il codice deve essere compilato da linea di comando usando il gcc