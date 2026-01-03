---
type: Uni Note
class: "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2024-12-09T16:13
updated: 2025-03-11T10:18
---
>[!abstract] Related
>- [[Input Output - Introduzione]]
>- [[Sistemi Operativi 1 (class)]]

---
## Introduzione

l problemi principali della gestione Input Output sono: 
- ci sono tantissimi dispositivi tutti molto diversi fra loro
- grande varietà di applicazioni che utilizzano questi dispositivi.

Per questo scrivere un S.O. in grado di gestirli tutti è quindi molto difficile.

Ma per iniziare possiamo dividere i dispositivi in 3 categorie:
- [[#^ce181b|Leggibili dall’utente]]
- [[#^80eb2c|Leggibili dalla macchina]]
- [[#^c814f0|Dispositivi di comunicazione]]

>[!note] Dispositivi Leggibili dall’Utente
>
>Sono i dispositivi utilizzati per la comunicazione con l’utente, come:
>
>- Stampanti
>- Terminali Hardware: Monitor, Tastiera, Mouse (da non confondere con i emulatori di terminali software dove eseguiamo comandi)
>
>In generale tutto quello che usa l’utente per dare informazioni al computer

^ce181b

>[!note] Dispositivi Leggibili dalla Macchina
>
>Dispositivi per la comunicazione leggibili in modo elettronico quindi ad esempio:
>
>- Dischi
>- Chiavette USB
>- Sensori
>- ecc…

^80eb2c

>[!note] Dispositivi di Comunicazione
>
>Dispositivi per la comunicazione leggibili in modo elettronico quindi ad esempio:
>
>- Dischi
>- Chiavette USB
>- Sensori
>- ecc…

^c814f0

---
## Funzionamento dei dispositivi I/O

>Un **dispositivo di input** è fatto in modo per essere interrogato sul valore di una grandezza al suo interno, ad esempio:
>
>- Il mouse può essere interrogato sul suo ultimo spostamento effettuato
>- La tastiera viene interrogata sul codice Unicode dei tasti premuti
>- Il disco vi dice i valori dei bit in una certa posizione
>
>Un processo che effettua una *syscall* `read` su un dispositivo vuole conoscere questo dato per poi eseguire delle azioni.

>Un **Dispositivo di Output** prevede di cambiare il valore di una certa grandezza fisica al suo interno. Ad esempio:
>
>- Un monitor prevede di cambiare il valore RGB dei suoi pixel
>- Una stampante il file da stampare
>- Un disco il valore dei bit da sovrascrivere in una certa posizione
>
>Un processo che effettua una _syscall_ `write` vuole cambiare qualche valore all’interno del dispositivo.

>[!note] System Calls e Kernel
>Il sistema operativo deve quindi offrire due _syscall_: `read` e `write`, tra gli argomenti di queste call ci sarà l’identificativo del dispositivo interessato, su Linux è chiamato _file descriptor_.
>
>Quando è eseguita una syscall, entra in gioco il kernel che comanda l’inizializzazione del trasferimento di informazioni in lettura o scrittura a seconda del caso, mette il processo in blocked. A questo punto al resto ci pensa il dispositivo I/O.
>
>La parte del kernel che gestisce un particolare dispositivo I/O si chiama **driver**, questo fornisce gli opportuni comandi al S.O. per controllare il dispositivo, spesso sono istruzioni macchina.
>
Il trasferimento dei dati spesso si fa con il [[Input Output - Introduzione#^d3d6d0|DMA]].
>
>A trasferimento completato arriva l’interrupt e il processo torna ready:
>- L’operazione di trasferimento potrebbe fallire
>- Potrebbe essere necessario fare ulteriori trasferimenti

---
## Differenze tra dispositivi I/O

I dispositivi di I/O possono differire sotto molti aspetti:
- [[#^fd974f|Data rate]]
- [[#^ad6c15|Applicazione]]
- [[#^20b1ec|Difficoltà nel controllo]]
- [[#^09751e|Unità di trasferimento dati]]
- [[#^9bae77|Rappresentazione dei dati]]
- [[#^518b86|Condizioni d'errore]]

>**Data Rate**
>È la velocità di trasferimento dei dati, ci sono dispositivi molto lenti e altri molto veloci
>
>![[3. MOCS/Uni MOC/archive/attachments/Pasted image 20241209165504.png|550]]

^fd974f

>**Applicazione**
>
>È il modo in cui i dispositivi I/O vengono usati, ad esempio
>-  I *dischi* sono usati per memorizzare files e richiedono un software per la gestione di quest’ultimi, ,a possono anche essere utilizzati per la memoria virtuale.
>- un *terminale* come tastiera e mouse usato da un amministratore dovrebbe avere priorità più alta.

^ad6c15

>**Complessità del controllo**
>
>La facilità fi controllo dei dispositivi I/O varia da dispositivo a dispostivo:
>
>- Tastiera e Mouse richiedono un controllo molto semplice.
>- Una stampante è più complessa dato che deve muovere molti macchinari per la stampa.
>- Il Disco è una delle cose più complesse da controllare.
>
>Tutto questo non si fa solo software ma anche con hardware dedicato.

^20b1ec

>**Unità di trasferimento dati**
>
>I dati possono essere trasferiti:
>- In ***blocchi di byte di lunghezza fissa***, usato ad esempio per memorie secondarie come dischi, chiavi USB ecc…
>- ***Flusso di byte (stream)*** o equivalentemente di caratteri, usato da qualsiasi cosa non sia memoria secondaria, quindi terminali hardware, dispositivi di comunicazione di rete ecc…

>**Rappresentazione dei dati**
>
>I dati sono rappresentati secondo codifiche diverse in dispositivi diversi, ad esempio tastiere possono usare *ASCII* o *UNICODE* o avere controlli di parità diversi.

>**Condizione d'errore**
>
>La natura degli errori varia da dispositivo a dispositivo:
>
>- Possono notificare gli errori in modo diverso
>- Conseguenze degli errori, possiamo avere errori fatali o altri ignorabili
>- Gestione degli errori