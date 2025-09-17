---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2025-09-14T13:45
updated: 2025-09-14T13:45
---
325 natale 2024


BD
Perchè applichiamo algoritmo decomposiziome che preserva dipendenze?

Dobbaimo controllare l'equivalenza di dipendenze di due insiemi di dipendenze funzionali, F di R e G della proiezione sugli attributi Ri di F.

Come è fatta la proi3zione di F su un sottoschema?
Prendiamo tutte le dipendenze di F+ che possono essere soddisfatte dall'istanza di un sottoschema

Cosa significa equivalenti?
La loro chiusura è uguale
Per fare ciò, lemma 2: basta verificare che F è contenuto in G+ e G è contenuto in F+ 

Cosa ci permette di utilizzare solo G contenuto in F+ e  non G+?

Il lemma 2, sulle chiusure, che ci dice che F è contenuto in G+ se F+ è contrnuto in G+

X+ di G come lo calcoliamo qui?

In input prendiamo la decomposizione, un sottoschema X dello schema di cui vogliamo calcolare la chiusura ed F di R.
Algoritmo spiegazione
Spiegazione dell'algoritmo deve essere secca e puntuale.
 Meno tempo ci passi sopra meglio andrà, non troppo poco pk presume che tu non sappia. Porcodio è tip9 la roba piu difficile della materia però quindi e un po un casino. Devi allenarti nell'espozione e comprendimento. Non ci mettere troppi riferimenti ad altra roba se non ne sei ravvero tanto convinto e sai di wuella roba. 
Ipotesi induttiva, cerca di capire quando si applica????
Perchè dobbiamo escludere dip banali?
0erchè ogni sottoinsieme di R determina a sua volta i suoi sottinsiemi anche se non sono attributi primi

Perchè prendiamo le dipendenze in  F+ ?


Altra roba
O x superchiave o y composto da attributi primi (vanno bene anche di chiavi diverse)


File ISAM;
Ordinamento sulle chiavi dei record, composto da file indice e file princ, i blocchi del file indice contengono solo chiave e puntatore, nel file principale i record. Chiavi e puntatori si vsnno a riferire ai "primi" blocchi del file principale, queste sezioni si fermano alla chiave contenuta nel prossimo putnatore nell'indiceq insomma questa se l'è scordata.

Abbiamo operazioni, ricerca binaria o per interpolazione; 


si fanno sul fiel indice, si prende il blocco a meta piu uno del fi e se è minore andiamo a controllare da 1 a m (!) e quindi includo ed escludo via via...
E se arrivi allultimo blocco del file principale e vedi che la chiave è minore xel coso che dta cercando. Posso eliminarlo dalla rixerca questo blocco?

 NO, i valori piu grossi saranno solo dopo quel blocco, se è da qualche parte sara lì pe forza

Codto di quesra rucerxa, log 2 bdbsjs

Costo minimo, medio o costante?

Costo madsimo, perchè???

AaaaaAAAA Poichè  . Pouchè m numero die blocchi. È il numero massimo di volte che posso dividere il numero per 2!!!!!! Porocdu

Ricerca per interpolazione?

Stiami cercando un chiave k1. Calcoliamo f() funzione che prende k1, k2 chiave di primo blocco e k3 chiave di ultimo blocco, moltiplichiamo per m n totale di blocchi file indice 

Che complex ha ricerca per interpilazione?
1 + log2 .... nn uo snetiot

Perchè se è così conveniente non la utilizzjamo?
 Me lo so perso me spiaz

Quali sono i probkemi che possiamo trovare alla base di un accesso rjke e come possiamo risolverli?

Aggiornamneto perso, quando una transazione accede ad un datoz loo modigica, la transazione accede ad un dato ma non legge la modifica pk la prima trans nn ha scritto. Come finidce la storia??? Finisce cue tutte le modifichesono state applicate da un dato noj corretto. Abbiamo i valori diversi r non sappiamo neanche chi abbiamo! A seconda di chi scrive per ultimo ..

Aggregato non corretto
Quando una transazione modifica un item e poi lo scrive. L'altra che doveva fa na somma e prendere il dato che doveva esse modificato ma è sfato modificato dalla prima trans , ne legge uno aggiornato e l'altro non

Dato sporco

Come si risolve?
Lock binario a due fasi stretto

Aggregato non corretto
Lock a due fasi

Aggiornamento perso
Lock

Abbiamo modo di controllare la concorrenza senza qurstr avariabili a lucchetto?
 Si ad esempio con timestanp

///////////
Sepe

Chiusura di un insimee di dioendenze?

Chiuusura id insiem di dipendenze?
Istanza he soddifa x det y?

Se due tuple sono uuali su x sono uguali su y.


Come lo so senza scriverlo sempre?
Assiomi di Armstrong
Assiomi applicabili partendo da F
1. Rifledsività
2. Transitivita vbb dai sono loro
3.aumento sè jncartato

Gulp
Ipotesi induttiva è che la basd non ci piace, visogna partire dla caso base

Fi i esima aoplicaziond di assiomi armstrong
F = Fa0 
perchè f è contenuto in f+? 
Perchè in F+ sono contenutr tutte le dipendenze funzionali cintenute in F e quelle in F sono sicuramente gia contenute

Al passo i-1 è contneuto in F+ ,, ipotesi induttiva (ogni dipendenza che appariene qui appartiene anche qui, qujndi è contneuto, ogni dipendenza che ottengo agteaverso armstrog è rispettata da ogni istanza legale. 

Basically F+ = FA
Dura tre anni la parte sukel dipendenze appena si esce da argomento dipendenze va molto molto più veloce l'orlae
Prima FA contentuo in F+, poi F+ contenuto in FA

Istanza banalmente legali?

Quandi una dipendrnza viene soddisfatta?
Wuando ho una sola tupla
Wuando ho 0 tuple

Se uno schema è in 3NF posso creare delle istanze che violano le dipendenze?
(Non ha più risposto alla domanda ma è da sottintendere, no)

Def di 3NF, una chiave è unica per ogni tupla, a partjà di chiave le tuple sono uguali

Possibile distinzione tra 3NF e Boyce Codd

1.Algoritmo
2.Teoria dipendneze
3.Struttura organizzazione fisica
4.Concorrenza

Parlami del B Tree
Le foglie sono il file principale, in ogni foglia ci sono record. 
Parto dal livello piu alto. Nel liv piu alto ho un singolo puntatore. Ho delle chiavi che smistano la richiesta... sta essendi un po confusionario ngl
Mella radice faccio una ricerca basata sulle chiavi. Che caratteristica ha la chiave associata al puntatore? 

Lq chiave del record RICOPRE tutte le xhiavi del sottoalbero.
Altezza dell'albero. Il blcoco a cui punta un record avrà tutte le chiavi contenute tra la sua e quella succrssiva, stiamo suddividendo i ntervalli in intervalli piu piccoli. Ci sono record che riesco a trovare prima? Stocazzo no è uguale per tutti domandaa a trabocchetto.

C'è qualcosa che puo influenzare altezza dell"albero?
I blocchi li prendiamo smepre per metà, se sono riempiti completamente l'altezza e minima.
Come stimiamo l'altezza massima di un btree?
Si, si puo stimare, siano D il minimo numero di recodd che posso inserire in un blocco nell' indice, sia E num record totali.
Una buona stima di auanfo sia alto albero è logn/d di n/e.
 Come ci arriviamkmmm?mm?m? 
Nel file prinxipale distribuiamo gli n record in modo tale che entrino nel piu piccolo spazio per essere considerato pirno per metà. È da vedere la spiegazione sulle slide è un casino prendere appunti cosi

Se io devo inserire un record in un b tree cosa devo fare?

Fo ricerca, fin quando arrivo al file pricnipale. Se nel blocco del file principale ce spazio insrrisco il record senza problemi. Sr è pieno, innanzitutto provo a vedetr se rirsco a inserirlo nel blocco successivo, ci metto dentro il record che devk inserire più altri valori da mettere nello scorso blocco, devo far scivolarr roba . Poi drvo collegarlo ad un file indice. Se anche il piano di sopra è pieno ripeto l'operazione. Nel caso peggiore sblocco ogni singolo blocco del piano di sopra, se devo farlo sulla radice allora aumenta altezza dell'albero e nsomma un casino


Mi parli dei timestamp?
I timestamp sono una tecnica che utilizziamo per rwndere serializzabkle una scheduke e lo facciamo assegnando ad ogni ......... 
Ha fatto confusione incredibile
Sono timestamp dell'ultima transazione che ha fatto accesso a qurll"item, con ultima intendiamo più GIOVANE.

 Nrl mofello di timestamp serializzabilità vuol dire?




BD 03/03
Primo, chi è primo? Attributo singolo
XdY in F con A primo
XdA in F+ con Y composto da elementi primi

Org Hash
È sempre vero che è 1/B esimo la ricerca su un bucket rispetto ad heap? Con condizione di buona funzione di hash
Costo nella heap? N/2, come ci arrivo?

Il punto di commit dove lo mettiamo, cos'è? Cosa deve aver già fatto per dire con sicurezza che noj può più essere abirtita? Riba sui deadlock
Deve anche aver finito di operare sulla sua area di lavoro
C'è un modo per evitare del tutto i deadlock?
Usando una versione padticolare xel protocollo a due fasi stretto, la versione conservativa. Come fa a evitare il deadlock?