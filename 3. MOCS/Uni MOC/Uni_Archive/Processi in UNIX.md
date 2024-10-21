---
type: Uni Note
class:
  - "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related: "[[Processi]]"
completed: true
created: 2024-10-20T15:08
updated: 2024-10-20T17:01
---
>[!abstract] Index
>1. [[#Esecuzione dei processi in UNIX]]
>2. [[#Il Processo Unix]]
>	1. [[#Livello Utente]]
>	2. [[#Livello Registro]]
>	3. [[#Livello Sistema]]
>3. [[#Creazione di un Processo in Unix]]

>[!abstract] Related
>- [[Processi]]
>- [[Sistemi Operativi 1 (class)]]

---
## Esecuzione dei processi in UNIX

Linux utilizza un misto tra [[#^1fa6c4|Kernel Interno ai Processi Utente]] e [[#^338496|Kernel Basato sui Processi]].

Le funzioni del Kernel sono eseguito per lo più tramite interrupt per conto del processo corrente, ma ci sono dei processi di sistema chiamati **kernel threads** che partecipano alla normale competizione del processore.

Di solito sono periodici, ed eseguono una specifica operazione come ad esempio:
- Riorganizzare la RAM liberando spazio
- Gestire dispositivi I/O
- Operazioni di rete

>[!note] Transizione tra Stati dei Processi
>![[Pasted image 20241020150852.png|550]]
>
>- **User Running:** in esecuzione in modalità utente
>- **Kernel Running:** in esecuzione in modalità kernel o sistema
>- **Ready to Run:** in Memory può andare in esecuzione non appena il kernel lo seleziona
>- **Asleep in Memory:** non può essere eseguito finch ́e un qualche evento non si manifesta; il processo è in memoria
>- **Ready to Run:** Swapped può andare in esecuzione (non è in attesa di eventi esterni), ma prima dovrà essere portato in memoria
>- **Sleeping o Swapped:** non può essere eseguito finché un qualche evento non si manifesta; il processo non è in memoria primaria
>- **Preempted:** il kernel ha appena tolto l’uso del processore a questo processo (preemption), per fare un context switch
>- **Created:** appena creato, ma ancora non pronto all’esecuzione
>- **Zombie** terminato, ma resta nelle tabelle dei processi perché il processo che l’ha creato possa prendersi il suo valore di ritorno

---
## Il Processo Unix

Il [[Processi#Proces Control Block (PCB)|PCB]] del processo UNIX è formato da 3 principali sezioni:
1. [[#Livello Utente]]
2. [[#Livello Registro]]
3. [[#Livello Sistema]]

>[!note]- Formato del PCB
>![[Pasted image 20241020153947.png|600]]
>
>- **Process Size:** Indica la dimensione dell’immagine del file e non quella del PCB, quest’ultimo ha grandezza predefinita.
>- **User Identification:** Ad esempio se un processo è in esecuzione utente e va in modalità kernel, l’effective user ID diventa il “sistema operativo” mentre il real user ID rimane l’utente iniziale.
>- **Event Descriptor:** Indica perché il processo è in asleep
>- **P_Link:** Puntatore al prossimo processo in coda (coda ready o altre code).

### Livello Utente
- **Process Text:** Codice Sorgente in linguaggio macchina
- **Process Data:** Sezione di dati del processo ovvero i collegamenti ai valori delle variabili
- **User Stack:** Le chiamate del processo
- **Shared Memory:** Memoria condivisa con altri processi se presente

^ecb2f3
### Livello Registro
- **Program Counter:** Indirizzo della prossima istruzione del process text da eseguire
- **Processor status register:** Registro di stato del processore, relativo a quando è stato swappato l’ultima volta
- **Stack Pointer:** puntatore alla cima dello user stack
- **General purpose registers:** Registri accessibili al programmatore, relativo a quando è stato swappato l’ultima volta.

^10236c
### Livello Sistema

- **Process table entry:** Puntatore alla tabella di tutti i processi che individua quello corrente
- **U Area:** Informazioni per il controllo del processo
- **Process Region Table:** Definisce il mapping tra indirizzi virtuali ed indirizzi fisici
- **Kernel Stack:** Lo stack di chiamate separato da quello utente usato per le funzioni di sistema.

---
## Creazione di un Processo in Unix

- Viene effettuata una chiamata di sistema `fork()`
- Il SO, in kernel mode:
    1. Alloca una entry nella tabella dei processi
    2. Assegna un [[PID]] al processo
    3. Copia l’immagine del padre escludendo la memoria condivisa, una volta fatto questo sia padre che figlio vorranno eseguire la stessa istruzione successiva al fork.
    4. Incrementa i contatori di ogni file aperto dal padre dato che ora sono anche del figlio
    5. Assegna al processo lo stato **Ready to Run**
    6. La fork ritorna il [[PID]] del figlio al padre e 0 al figlio, nello specifico all’interno del codice posso inserire un _if_ sul valore della fork, se è 0 sono nel figlio e posso eseguire le istruzioni che voglio, se non è 0 sono il padre e allora posso continuare con le vecchie istruzioni oppure ad esempio aspettare la terminazione del figlio.

Quindi quando creiamo un processo figlio, inizialmente questo è una copia del padre, si è notato che è la cosa più efficiente dato che è la situazione più comune quella dove un figlio esegue una parte del codice del padre.

Una volta creato, il kernel decide se continuare ad eseguire il padre, eseguire il figlio o un altro processo ancora.
