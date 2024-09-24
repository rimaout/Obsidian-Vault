---
type: Uni Note
class: 
academic year: 2023/2024
related: 
completed: false
created: 2024-09-24T15:36
updated: 2024-09-24T17:16
---
>[!abstract] Index
>1. 

>[!abstract] Related
>- 

---

Il sistema operativo si occupa di gestire le risorse hardware di un sistema, come:
- uno o più processori
- memoria primaria (RAM)
- dispositivi di input/output
	- memoria secondaria (dischi)
	- rete

>[!tip] Componenti di un sistema monoprocessore
>![[Pasted image 20240924155823.png|500]]

## Componenti del processore
- Processore: il cervello del computer: si occupa di tutte le computazioni
- Memoria Principale: volatile se si spegne il computer, se ne perde il contenuto talvolta chiamata memoria reale o primaria
- Moduli di input/output
	- dispositivi di memoria secondaria (dischi...), non volatile
	- dispositivi per la comunicazione (schede di rete...)
	- altri dispositivi: tastiera, monitor, stampante, mouse, ...
- “Bus” di sistema mezzo per far comunicare tra loro le parti interne del computer:
processori, memoria principale, e moduli di input/output

## Registri del processore
- Registri visibili dall'utente
	- usati o da chi programma in assembler o dai compilatori di linguaggi non interpretati
	- obbligatori per alcune istruzioni su alcuni processori
	- facoltativi per ridurre accessi alla memoria principale
	- linguaggi compilati (“vecchi”): C, C++, Fortran; linguaggi
	- interpretati (“nuovi”): Python, Java
- registri di controlli e di stato
	- usati dal processore per controllare l’uso del processore stesso
	- usati da funzioni privilegiate del SO per controllare l’esecuzione dei programmi
- Registri "interni":
	- usati dal processore tramite microprogrammazione
	- comunicazione con memoria ed I/O 
### Registri visibili all'utente
- Gli unici che possono essere usati direttamente (con il loro nome) quando si programma in linguaggio macchina
- Possono contenere dati o indirizzi
- Possono contenere dati o indirizzi:
	- Possono contenere dati o indirizzi
	- registri-indice: per ottenere l’indirizzo effettivo, occorre aggiungere il loro contenuto ad un indirizzo base

xcklkasjzblònaljsvnzlkòccjalkjlkckn

### Registri di Controllo e di stato



---
### Interruzioni 
- Paradigma dell’interazione hardware/software
- Interrompono la normale esecuzione sequenziale del processore

Esistono 2 tipi
- Sincrone: eccezioni che vengono chiamate immediatamente dopo l'esecuzione di una certa istruzione
- Asincrone:

### Interruzioni Sincrone



Le systemcall sono interazioni sincrone che non causano l’interruzione del programma.


>[!warning] Fasi di Interruzione
>![[Pasted image 20240924163458.png|500]]
>
>- Ad ogni ciclo fetch-execute, viene anche controllato se c'è stata un’interruzione (o una exception)
>- Se così è, il programma viene sospeso e viene eseguita una funzione che gestisce l’interruzione (interrupt-handler routine)


