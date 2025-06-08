---
type: Uni Note
class: "[[Reti (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2025-04-29T14:27
updated: 2025-06-08T12:00
---
## Introduzione

Questo protocollo è basato sull'idea di **Link State**, ovvero il costo associato al link (collegamento), in particolare:
- $\infty$ indica un collegamento inesistente o interrotto
- Ogni nodo deve conoscere i costi di tutti i collegamenti della rete
 
Per la memorizzazione di queste informazioni è utilizzato un [[#Link State Database (LSDB)]].

>***oss:*** è un alternativa al [[RIP - Routing Protocol Intra-Domino#Algoritmo d’instradamento con vettore distanza (Distance Vector - DV)|distance vector (DC)]] utilizzato in [[RIP - Routing Protocol Intra-Domino|RIP]].

## Link State Database (LSDB)

Il link state database mantiene la *mappa completa della rete*, *ogni nodo ne mantiene una copia* e deve essere *univoco* (uguale) tra tutti i nodi della rete.

>[!note] Rappresentazione
>
>É rappresentato attraverso una matrice dove `M[x][y]`contiene il costo del collegamento tra il nodo `x` e il nodo `y`.
>
>![[Pasted image 20250429145002.png|700]]

>[!note] Creazione (flooding)
>
>Ogni nodo della rete deve innanzitutto conoscere i propri vicini e i costi dei collegamenti verso di loro, per fare ciò:
>- ogni nodo invia un messaggio di `hello` a tutti i suoi vicini.
>- ogni nodo riceve gli `hello` dei vicini e crea la lista dei vicini chiamata **LS Packet (LSP)** contenente tuple `(vicino, costo)`.
>
>Ogni nodo esegue un **flooding**, ovvero:
>- Invia a tutti i vicini il proprio LSP.
>- Quando riceve LSP da un vicino, se è nuovo allora lo inoltra anche ai suoi vicini, eccetto quello da cui lo ha ricevuto.
>- In questo modo aggiorniamo tutta la rete.
>
>Una volta terminato questo processo abbiamo costruito l’LSDB.
>
>![[Screenshot 2025-05-18 at 10.06.16.png|900]]

^6987b0

^4c98a5
## Algoritmo Link State (LS)

Per costruire il suo albero a costo minimo utilizzando il LSDB ogni nodo deve eseguire l’**algoritmo di Dijkstra**, in modo indipendente, scegliendo se stesso come nodo radice.

Definiamo la seguente notazione:
- $N$: insieme di nodi della rete.
- $c(x,y)$: costo collegamento dal nodo `x` al nodo `y`.
- $D(v)$: costo del cammino minimo dal nodo origine alla destinazione `v` (nel iterazione corrente).
- $p(v)$: immediato predecessore del nodo `v` lungo il cammino minimo.
- $N'$: sottoinsieme dei nodi per cui il cammino a costo minimo dall'origine è definitivamente noto.

>[!note] Inizializzazione
>
>Prima di utilizzare l'algoritmo di Dijkstra, dobbiamo inizializzare il sottoinsieme di nodi adiacenti alla radice:
>
>```
>N' = {r}
>for all nodi n in N:
>	se n è adiacente a r
>		allora D(n) = c(r,n)
>	altrimenti D(n) = inf
>```

>[!note] Ciclo
>
>Una volta inizializzato il sottoinsieme con i nodi adiacenti alla radice, possiamo far partire il ciclo:
>
>```
>determina un `n` non in N' tale che D(n) sia minimo
>
>aggiungi `n` a N'
>
>per ogni nodo `a` adiacente a `n` e non in N' aggiorna D(a):
>	D(a) = min(D(a), D(n) + c(n, a))
>Termina quando N' = N
>```

Possiamo applicare Dijkstra per risolvere esercizi in modo “grafico”:
![[Pasted image 20250607163417.png|1200]]

Quindi ad ogni step aggiorniamo i costi per ogni nodo e allo step successivo aggiungiamo in `N'` il nodo con costo minimo.

Al termine della procedura otteniamo, l'albero dei percorsi minimi che collega il nodo radice a tutti i nodi della rete.

![[Pasted image 20250607164231.png|850]]
## Confronto tra algoritmi LS e DV

>[!note] Complessità
>
>Con algoritmi [[#Algoritmo Link State (LS)|LS]] se abbiamo `n` ed `E` collegati implica l'invio di `O(nE)` messaggi.
>
>Con un algoritmo [[RIP - Routing Protocol Intra-Domino|DV]] è richiesto lo scambio di informazioni soltanto tra i nodi adiacenti, e quindi il tempo di convergenza è potenzialmente più basso, ma può variare.

>[!note] Velocità di convergenza
>
>Con algoritmi [[#Algoritmo Link State (LS)|LS]] abbiamo complessità di $O(n^{2})$, dato che procede prima `n` nodi, poi `n-1`, `n-2`, etc , quindi `n(n+1)/2`.
>
>Con algoritmi [[RIP - Routing Protocol Intra-Domino|DV]] abbiamo una convergenza più lenta, dato che:
>- può presentare cicli d’instradamento
>- può presentare il problema del conteggio all’infinito (lo scambio di aggiornamenti infinito)

>[!note] Robustezza
>
>In generale l’OSPF ([[#Algoritmo Link State (LS)|LS]]) è più robusto di RIP ([[RIP - Routing Protocol Intra-Domino|DV]]), infatti cosa succede se un router funziona male?
>
>
>Con OSPF che si basa su [[#Algoritmo Link State (LS)|LS]], se un router comunica a tutti un costo sbagliato per uno dei suoi collegamenti non compromette l’intera rete dato che ogni nodo calcola la tabella localmente.
>
>Com RIP che si basa su [[RIP - Routing Protocol Intra-Domino|DV]], se un router comunica cammini errati significa che questa informazioni si diffonde su tutta la rete portando a calcoli errati.

## Approfondimento Protocollo OSPF (Open Shortest Path First)

Fino ad ora abbiamo visto un algoritmo, ma un protocollo è composto da molto altro, infatti deve definire 
- il suo ambito di funzionamento
- i messaggi che vengono scambiati
- la comunicazione tra router
- l’interazione con gli altri protocolli.

In particolare vediamo il protocollo OSPF (Open Shortest Path First) basato su [[#Algoritmo Link State (LS)]].

>***Nota:*** si dice open perché le sue specifiche sono pubblicamente disponibili.

Questo è un protocollo a stato del collegamento, ovvero:
- Utilizza il [[#^6987b0|flooding]] di informazioni di stato del collegamento.
- Utilizza Dijkstra ([[#Algoritmo Link State (LS)|algoritmo LS]]) per la determinazione del percorso a costo minimo.

>[!note] Flooding in OSPF
>
>Nel OSPF, ogni volta che si verifica un cambiamento nello stato di un collegamento, il router manda informazioni d’instradamento a tutti gli altri router, utilizzando la tecnica del [[#^6987b0|flooding]].
>
>Invia periodicamente (ogni 30 minuti) messaggi OSPF all’intero sistema autonomo, utilizzando il [[#^6987b0|flooding]].

>[!note] Messaggi OSPF
>
>- ***Hello*** - Usato dai router per annunciare la loro esistenza ai vicini
>- ***Database Description*** - Risposta ad hello, di solito per inviare il LSDB ai nuovi router
>- ***Link State Request*** - Usato per richiedere specifiche informazioni su un collegamento
>- ***Link State Update*** - Messaggio principale usato da OSPF per la costruzione del LSDB
>- ***Link State ACK*** - Riscontro al link state update (offre più affidabilità)
>
>>***Nota:*** I messaggi OSPF vengono trasportati direttamente in datagrammi IP usando il numero di protocollo 89 nel campo IP protocol.
