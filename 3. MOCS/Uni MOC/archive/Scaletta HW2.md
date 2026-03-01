---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2026-02-16T09:53
updated: 2026-02-16T13:16
---
## 

**Parametri:**
• il nome di un file (potrebbe essere un file di testo o binario, ma al fine della verifica del funzionamento sarà utile un file di testo)
• una chiave K di lunghezza 64 bit (rappresentabile mediante un intero di tipo unsigned long long int) 
• un intero p che determina il grado di parallelismo desiderato nel calcolo della cifratura
• l’indirizzo IP del server ed il numero di porta su cui il server è in ascolto

**Quando leggiamo il file non serve il padding, perche il server legge esattamente la dimensione del file***

Requisiti del processo Client

• Il client deve utilizzare al più p thread per eseguire le operazioni di cifratura in parallelo.
• Il client deve gestire correttamente la chiusura della connessione da parte del server. (***facciamo il free***)
• Il processo client, quando effettua le operazioni di cifratura e di invio non deve essere interrotto da (SIGINT, SIGALRM, SIGUSR1, SIGUSR2, SIGTERM).
• L’uso di eventuali strutture dati condivise tra thread deve essere progettato in modo da evitare race conditions.

Specifica del processo Server
L’applicazione server riceve come input


• un intero p che determina il grado di parallelismo desiderato nel calcolo della decifratura
• una stringa s che costituisce un prefisso per il nome dei file di output
• un intero l che indica il numero di connessioni che possono essere concorrentemente gestite dal server.

Il processo server si pone in ascolto su di una specifica porta ed accetta richeste di connessione da più processi client.
Il server riceve dal client un messaggio contenente un testo cifrato C, la lunghezza del testo cifrato L e la chiave di cifratura K (64 bit). Il server estrae queste informazioni dal messaggio, divide C in n blocchi di dimensione 64 bit e, facendo uso di p thread (p<=n) decifra il messaggio calcolando il bitwise XOR tra K ed ogni blocco Ci per ottenere Bi = Ci XOR K.

I thread memorizzano I blocchi decifrati in un buffer condiviso. Dopo che il messaggio è stato completamente decifrato e ricostruito concatenando gli n blocchi Bi, viene salvano su di un file il cui nome inizia con il prefisso s.

Dopo aver terminato l’operazione di decifratura, ma prima di aver scritto sul file, il processo invia l’acknowledgement al client e chiude la connessione con il client.

Requisiti del server

• un thread del processo server che sta decifrando un messaggio C non deve essere interrotto da segnali (SIGINT, SIGALRM, SIGUSR1, SIGUSR2, SIGTERM).
• Un thread del processo server che sta scrivendo il testo decifrato su disco non deve essere interrotto dal segnali (SIGINT, SIGALRM, SIGUSR1, SIGUSR2, SIGTERM)
• Il buffer condiviso per la memorizzazione del testo decifrato deve essere allocato dinamicamente, gestito come una lista concatenata di blocchi, e le race condition devono essere evitate.

Requisiti generali


• I parametri delle applicazioni client e server devono essere passata come parametri da linea di commando, oppure come valori di variabili di ambiente
• Le applicazioni client e server devono gestire correttamente gli errori nei parametri di input, ma anche tutti i possibili errori di chiamata a funzioni e system call

Esempio di cifratura
F=”il mio nome e’ legenda”

Rappresentazione binaria
01001001 01101100 00100000 01101101 01101001 01101111 
00100000 01101110 01101111 01101101 01100101 00100000 
01100101 00100111 00100000 01101100 01100101 01100111 
01100101 01101110 01100100 01100001

L=22 byte = 172 bit

K=”emiliano”
Rappresentazione binaria
01100101 01101101 01101001 01101100 01101001 01100001 01101110 01101111

n=3 blocchi, il terzo va riempito con 16 bit. Mettiamo tutti 0

B1 = 01001001 01101100 00100000 01101101 01101001 01101111 00100000 01101110
B2 = 01101111 01101101 01100101 00100000 01100101 00100111 00100000 01101100
B3 = 01100101 01100111 01100101 01101110 01100100 01100001 00000000 00000000

C1 = B1 XOR K =
01001001 01101100 00100000 01101101 01101001 01101111 00100000 01101110
XOR
01100101 01101101 01101001 01101100 01101001 01100001 01101110 01101111
=
00101100 00000001 01001001 00000001 00000000 00001110 01001110 00000001


Testing

• progettare una serie di casi di test che permettano di verificare le specifiche ed i requisiti del processo client e server