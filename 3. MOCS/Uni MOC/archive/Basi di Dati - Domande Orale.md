---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2025-02-24T17:45
updated: 2025-09-17T09:20
---
[Link raccolta aglaia](https://aglaianorza.github.io/notesig/vault/basi-di-dati-1/domande-orale,-raccolte)

## Domanda prese da me



---

[[Domando Orale BD1 Mie]]
[[Domande Orale BD1 Dado]]

**Definizione di Chiave**
Una _chiave_ di una relazione è un attributo o un insieme di attributi che identifica univocamente una tupla

Dati uno schema di relazione R e un insieme F di dipendenze funizonali, un sottoinsieme K di uno schema di relazione R è una _chiave_ di R se:
- $K \rightarrow R \in F^+$ (se soddisfa solo questo punto è una _superchiave_)
- non esiste un sottoinsieme proprio di $K'$ di $K$ tale che $K' \rightarrow R \in F^+$

**Cos'è uno schema di relazione?**
Uno schema di relazione R è un insieme di attributi $\{A1, A2, ..., An\}$

**Cos'è un'istanza di uno schema?**
Dato uno schema di relazione R una _istanza_ di R è un insieme di tuple su R

**Cos’è una tupla?**
Una tupla t su R è una funzione che associa ad ogni attributo $A_i$ in R un valore $t[A_i]$ nel corrispondente dominio dom($A_i$)

**Definizione di Dipendenza funzionale**
Dato uno schema di relazione R una _dipendenza funzionale_ su R è una coppia ordinata di sottoinsiemi non vuoti X ed Y di R e viene denotata come $X \rightarrow Y$.

- X determina funzionalmente Y  
- Y dipende funzionalmente da X 
- X = parte sinistra della dipendenza o determinante 
- Y = parte destra della dipendenza o dipendente

**Cosa vuol dire che un’istanza r soddisfa la dipendenza X → Y?**
Diciamo che un’istanza r di R soddisfa la dipendenza funzionale $X \rightarrow Y$ se per ogni coppia di tuple $t_1$ e $t_2$ di r si ha che se $t_1[X] = t_2[X]$ allora $t_1[Y] = t_2[Y]$

Le dipendenze funzionali servono ad esprimere dei vincoli su dei dati

**Quali sono le dipendenze funzionali banali?**
Se $Y \subseteq X, X \rightarrow Y \in F^+$ è detta banale

**Quale proprietà è possibile derivare dal concetto di dipendenze funzionali banali?**
$X \rightarrow Y \in F^{+} \leftrightarrow \forall A \in Y, X \rightarrow A \in F^+$

**Cosa vuol dire che un’istanza di R è legale?**
Dati uno schema di relazione R e un insieme F di dipendenze funzionali, un’istanza di R è legale se soddisfa tutte le dipendenze in F.

Dato uno schema di relazione R e un insieme F di dipendenze funzionali su R ci sono delle dipendenze funzionali che non sono in F, ma che sono soddisfatte da ogni istanza legale di R

**Qual è la definizione di chiusura di un insieme di dipendenze funzionali?**
Dato uno schema di relazione R e un insieme F di dipendenze funzionali su R, la _chiusura di F_ è l'insieme delle dipedenze funzionali che sono soddisfatte da ogni istanza legale di R

Si esprime con la notazione $F^+$

**Che rapporto esiste tra $F$ e $F^+?$
$F \subseteq F^+$

**Introduzione di $F^A$**
Denotiamo con $F^A$ l'insieme di dipendenze funzionali definito nel modo seguente:
- se $f \in F$ allora $f \in F^A$
- se $Y \subseteq X \subseteq R$ allora $X \rightarrow Y \in F^A$ _assioma della riflessività_
- se $X \rightarrow Y \in F^A$ allora $XZ \rightarrow YZ \in F^A$, $\forall Z \subseteq R$  _assioma dell'aumento_
- se $X \rightarrow Y \in F^A$ e $Y \rightarrow Z \in F^A$ allora $X \rightarrow Z \in F^A$ _assioma della transitività_

Dimostreremo che $F^{+}= F^A$, cioè che la chiusura di un insieme di dipendenze funzionali F può essere ottenuta a partire da F applicando ricorsivamente gli assiomi della riflessività, dell’aumento e della transitività, conosciuti come _assiomi di Armstrong_

**Conseguenze degli assiomi di Armstrong**
Queste tre regole che introduciamo ci consentono di derivare da dipendenze funzionali in $F^A$ altre dip. funz. in $F^A$

- se $X \rightarrow Y \in F^A$ e $X \rightarrow Z \in F^A$ allora $X \rightarrow YZ \in F^A$ **regola dell'unione**
- se $X \rightarrow Y \in F^A$ e $Z \subseteq Y$ allora $X \rightarrow Z \in F^A$ **regola della decomposzione**
- se $X \rightarrow Y \in F^A$ e $WY \rightarrow Z \in F^A$ allora $WX \rightarrow Z \in F^A$ **regola della pseudotransitività**

**Dimostazioni delle conseguenze degli assiomi**
![[DimostrazioneConseguenzeAssiomi.png|600]]

**Chiusura di un insieme di attributi**
_Definizione_
Siano R uno schema di relazione, F un insieme di dipendenze funzionali su R e X un sottoinsieme di R.
La chiusura di X rispetto ad F, denotata con $X_F^+$ , o semplicemente con $X^+$, è definita nel modo seguente 
$X_F^+$ $= \{A|X \rightarrow A \in F^A\}$

In pratica fanno parte della chiusura di un insieme di attributi X tutti quelli che sono determinati funzionalmente da X eventualmente applicando gli assiomi di Armstrong

$X \subseteq X_F^+$ (riflessività) o uguale alla sua chiusura se X non determina nessun'altro attributo

**Lemma 1**
Siano R uno schema di relazione ed F un insieme di dipendenze funzionali su R.
Si ha che: $X \rightarrow Y \in F^A$ se e solo se $Y \subseteq X^+$

_Dimostazione_
Sia $Y = A_1, A_2,...,A_n$
_Parte del se_
Poichè $Y \subseteq X^+$, per ogni $i, i=1,...,n$ si ha che $X \rightarrow A_{i} \in F^A$
Pertanto, per la regola dell'unione, $X \rightarrow Y \in F^A$

_Parte del solo se_
Poichè $X \rightarrow Y \in F^A$, per la regola della decomposizione si ha che, per ogni $i, i=1,...,n$ $X \rightarrow A_{i}\in F^{A}$ cioè $A_{i}\in X^+$, per ogni $i, i=1,...,n$ e quindi $Y \subseteq X^+$

**Teorema $F^{+}= F^A$**
Dimostreremo che $F^{+}= F^A$, cioè che la chiusura di un insieme di dipendenze funzionali F può essere ottenuta a partire da F applicando ricorsivamente gli assiomi della riflessività, dell’aumento e della transitività, conosciuti come assiomi di Armstrong.

_Dimostrazione_
Dimostro che i due insiemi sono uguali dimostrando la doppia inclusione
$F^{A} \subseteq F^{+} \land F^{+}\subseteq F^A$

_Prima Parte_
$F^{A} \subseteq F^+$

Sia $X \rightarrow Y$ una dipendenza funzionale in $F^A$.
Dimostro che $X \rightarrow Y \in F^+$  per induzione sul numero i di applicazioni di uno degli assiomi di Armstrong

_CASO BASE $i = 0$_
In tal caso $X \rightarrow Y \in F \implies X \rightarrow Y \in F^+$ perchè per definizione $F^+$ contiene tutte le dip. funz di $F$

_i = i-1 IPOTESI INDUTTIVA_
Per l’ipotesi induttiva ogni dipendenza funzionale ottenuta a partire da F applicando gli assiomi di Armstrong un numero di volte minore o uguale a i–1 è in $F^+$

$X \rightarrow Y \in F^{A} \implies X \rightarrow Y  \in F^+$  $X \rightarrow Y$ soddisfatto da ogni istanza legale

_i PASSO INDUTTIVO_
Bisogna dimostrare che la proprietà vale qualsiasi sia l'assioma applicato

1) Riflessività
$X \rightarrow Y$ è stata ottenuta applicando l'assioma della riflessività. In tal caso $Y \subseteq X$.
Sia r un'istanza di R e siano siano $t_1$e $t_2$ due tuple di r tali che $t_1[X] = t_2[X]$ banalmente si ha $t_1[Y] = t_2[Y]$

_Spiegazione_
Questa parte della dimostrazione sta verificando che se una dipendenza funzionale $X \to Y$  è stata ottenuta applicando la riflessività, allora essa è valida in ogni istanza e quindi appartiene a $F^+$.
Dato che $Y \subseteq X$, significa che ogni attributo in Y è già contenuto in X, quindi se $t_1$ e $t_2$ hanno gli stessi valori per $X$, avranno automaticamente gli stessi valori anche per Y (perchè gli attributi sono inclusi in X)

1) Aumento
$X \rightarrow Y$ è stata ottenuta applicando l'assioma dell'aumento ad una dipendenza funzionale $V \to W$ in $F^A$, ottenuta a sua volta applicando ricorsivamente gli assiomi di Armstrong un numero di volte minore o uguale a $i-1$ (quindi per ipotesi induttiva $V \to W \in F^+$)
Per costruzione dell'assioma $X$ e $Y$ devono essere stati creati aggiungendo un insieme Z agli insiemi di partenza $V \to W$
quindi possiamo porre $X = VZ$ e $Y = WZ$, con $Z \subseteq R$.
Sia r un'istanza legale di R e siano $t_1$ e $t_2$ due tuple di r tali che $t_1[X]=t_2[X]$, banalmente si ha che $t_1[V]=t_2[V]$ e $t_1[Z]=t_2[Z]$.
Usando l'ipotesi induttiva, da $t_1[V]=t_2[V]$ segue $t_1[W]=t_2[W]$
Da $t_1[W]=t_2[W]$ e $t_1[Z]=t_2[Z]$ otteniamo che $t_1[WZ]=t_2[WZ]$ da cui segue che $t_1[Y]=t_1[Y]$

1) Transitività 
$X \to Y$ è stata ottenuta applicando l'assioma della transitività a due dipendenze funzionali $X \to Z$ e $Z \to Y \in F^A$, ottenute a loro volta applicando ricorsivamente gli assiomi di Armstrong un numero di volte minore o uguale a $i-1$ (quindi per ipotesi induttiva $X \to Z$ e $Z \to Y \in F^+$)

Sia r un'istanza legale di R e siano $t_{1}$ e $t_2$ due tuple di r tali che $t_1[X]=t_2[X]$. Per ipotesi induttiva da $t_1[X]=t_2[X]$ segue $t_1[Z]$, ancora per ipotesi induttiva segue $t_1[Y]=t_2[Y]$

_Seconda Parte_
$F^{+}\subseteq F^A$

Per dimostrare questa parte si suppone per assurdo che esista una dip. funzionale $X \to Y \in F^+$ tale che $X \to Y \notin F^A$
Useremo una particolare istanza legale di R per dimostrare che questa supposizione porta ad una contraddizione.

Consideriamo la seguente istanza r di R

![[DimFa=F+.png|600]]

In questa istanza ci sono solo due tuple, uguali su $X^+$ e diverse su $R-X^+$

Dimostriamo che l'istanza è legale.
Utilizzando questa istanza dimostreremo che se $X \to Y \in F^+$ avremo necessariamente $X \to Y \in F^A$

_Spiegazione_
Nella dimostrazione per assurdo (in cui si prova che  $F^+ \subseteq F^A$ ), il ragionamento consiste nel costruire un’istanza  r  che è legale rispetto a $F^A$ , ma che viola una dipendenza funzionale specifica  $X \to Y$  che appartiene a  $F^+$  ma non a $F^A$

In pratica:
- Gli attributi di  $X^+$  (determinati da  $F^A$) sono uguali tra le tuple $t_1$  e  $t_2$ , perché questo garantisce che l’istanza rispetta le dipendenze in  $F^A$
- Gli attributi di $R-X^+$  (non determinati da $X^+$  in $F^A$) possono essere arbitrari, proprio perché $F^A$ non include $X \to Y$. Di conseguenza, la costruzione è _legale rispetto a_ $F^A$.

_Contraddizione_
Alla fine, si mostra che, nonostante la costruzione dell’istanza,  $X \to Y$ deve comunque essere soddisfatta anche se non era esplicitamente in  $F^A$. Questo significa che $F^+$ non può includere dipendenze funzionali che $F^A$  non ha già, e quindi $F^+ \subseteq F^A$

_Dimostrazione vera e propria_
Mostriamo che:
1) r è un'istanza legale di R (quindi soddisfa tutte le dipendenze in $F^A$)
Sia $V \to W$ una dipendenza funzionale in F

_Caso tuple diverse su V_
Se le due tuple sono diverse su V, allora la dipendenza è soddisfatta, perchè non si richiede nulla sulle componenti W quando le tuple sono già diverse su V

_Caso tuple uguali su V_
Ricordiamo che l'istanza di r è stata costruita in modo tale che:
1) le due tuple sono uguali solo sugli attributi in $X^+$
2) gli attributi al di fuori di $X^+$ possono essere diversi

Dato che le due tuple sono uguali su V, ne consegue che $V \subseteq X^+$, perchè le tuple sono uguali solo su quell'insieme di attributi.
Per il Lemma 1 si ha che se $V \subseteq X^+$, allora $X \to V \in F^A$, per l'assioma della transitività inoltre dato che $X \to V$ e $V \to W$, allora $X \to W \in F^A$, quindi, sempre per il Lemma 1 $W \subseteq X^+$ quindi le tuple sono uguali anche sui valori di W. 
Quindi $V \to W$ è soddisfatta e possiamo dunque dire che r è un'istanza legale poichè qualsiasi dipendenza in F è soddisfatta da r.

1) Abbiamo dimostrato che r è un'istanza legale, ora mostriamo che $X \to Y \in F^{+}\implies X \to Y \in F^A$
Poichè le dipendenze in $F^+$ sono soddisfatte da ogni istanza legale allora r soddisfa $X \to Y \in F^+$
Abbiamo due tuple uguali su X? Si poichè $X \subseteq X^+$ (per l'assioma della riflessitività e il Lemma 1) le due tuple di r coincidono sugli attributi di X, quindi poichè soddisfa $X \to Y$, devono coincidere anche sugli attributi di Y. Questo implica che $Y \subseteq X^+$ e per il Lemma 1 che $X \to Y \in F^A$

Note importanti usate per la dimostrazione:
- Se un'istanza è legale allora soddisfa anche tutte le dipendenze in $F^+$, anche perchè la definizione di $F^+$ è proprio l'insieme delle dipendenze soddisfatte da un'istanza legale
- $Y \subseteq X^{+}\leftrightarrow X \to Y \in F^A$, che come abbiamo visto equivale a dire che $Y \subseteq X^{+}\leftrightarrow X \to Y \in F^+$ e in particolare che $X \to Y$ deve essere soddisfatta da ogni istanza legale

**Perchè è esponenziale il calcolo di $F^{A}$?**
Il calcolo di $F^A$ (e quindi anche di $F^+$) richiede tempo esponenziale poichè ogni possibile sottoinsieme di R porta a una o più dipendenze, e i possibili sottoinsiemi sono $2^n$ dove n è il numero di attributi in R.
Quindi là complessità è legata alle dimensioni di R perchè il numero di sottoinsiemi di R cresce esponenzialmente.

**Definizione di 3NF**
Dati uno schema di relazione R e un insieme di dipendenze funzionali F su R, R è in 3NF se
$$\forall X \rightarrow A \in F^{+}, A \not \in X$$
- A appartiene ad una chiave (è _primo_)
oppure
- X contiene una chiave (è una _superchiave_)

_Nota_
La condizione $A \notin X$ è importante, poichè per l'assioma della riflessività, se $A \in X$, avremo sempre $X \to A \in F^{A} \implies X \to F^+$, anche quando A non è primo e X non è superchiave, se considerassimo queste dipendenze nessuno schema risulterebbe essere in 3NF

**Dipendenze parziali e transivite**
Siano R uno schema di relazione e F un insieme di dipendenze funzionali su R

$X \rightarrow A \in F^{+}| A\not \in X$ è una _dipendenza parziale_ su R se A non è primo ed X è contenuto propriamente in una chiave di R

_Esempio_
Ad un numero di matricola corrisponde un solo cognome Matr $\to$ Cogn
Ad una coppia costituita da un numero di matricola e da un codice di corso corrisponde un solo cognome
Matr C# $\to$ Cogn. Quest'ultima dipendenza funzionale è una conseguenza della dipendenza funzionale Matr $\to$ Cogn e viene detta dipendenza parziale

$X \rightarrow A \in F^{+}| A \not \in X$ è una _dipendenza transitiva_ su R se A non è primo e per ogni chiave K di R si ha che X non è contenuto priopriamente in K e $K-X \neq \emptyset$

_Esempio_
Studente (Matr, CF, Cogn, Nome, Data, Com, Prov)

Ad un numero di matricola corrisponde un solo comune di nascita: Matr $\rightarrow$ Com
Un comune si trova in una sola provincia: Com $\rightarrow$ Prov

Quindi ad un numero di matricola corrisponde una sola provincia: Matr $\rightarrow$ Prov

Matr $\rightarrow$ Prov viene detta dipendenza transitiva

**Definizioni Alternative di 3NF**
1) Dato uno schema R e un insieme di dipendenze funzionali F, R è in 3NF se e solo se non ci sono attributi che dipendono parzialmente o transitivamente da una chiave.

_Definizioni_
A _dipende parzialmente_ da una chiave K se $\exists X \subset R$ tale che $X \to A \in F^+$ con $A \notin X$ e tale che $X \subset K$ e A non è parte di chiave

A _dipende transitivamente_ da una chiave K se $\exists X \subset R$ tale che $K \to X \in F^+$ e $X \to A \in F^+$ e X non è una chiave e A non è parte di una chiave

1) Dato uno schema R e un insieme di dipendenze funzionali F su R, R è in 3NF se e solo se in F non ci sono né dipendenze parziali né dipendenze transitive.

**Forma Normale di Boyce-Codd**
È una forma più restrittiva rispetto alla 3NF

_Definizione_
Una relazione è in forma normale Boyce-Codd (BCNF) quando in essa _ogni determinante è una superchiave_

Una relazione che rispetta la forma Boyce-Codd rispetta la 3NF, ma non vale necessariamente l'opposto.

_Nota_
Può non essere possibile decomporre uno schema non BCNF ottenendo sottoschemi BCNF e preservando allo stesso tempo tutte le dipendenze, mentre questo è sempre possibile per la 3NF

**Decomposizione**
Quando si decompone uno schema per ottenerne uno in 3NF occorre tenere presenti altri due requisiti dello schema decomposto:

- la decomposizone deve _preservare le dipendenze funzionali_ che valgono su ogni istanza legale dello schema originario
- bisogna assicurarsi che il join delle istanze risultanti dalla decomposizione non riveli _perdita di informazione_, per perdita non si intende necessariamente informazioni in meno, ma anche aggiunta di informazioni estranee

Le dipendenze funzionali che si vogliono preservare sono tutte quelle che sono soddisfatte da ogni istanza legale di R, cioè
le dipendenze funzionali in F+, quindi si è interessati al calcolo di $F^{+}$ , ma questo richiede tempo esponenziale in $|R|$

**Algortimo -  Calcolo della chiusura di un insieme di attributi X**
(continuo della parte precedente)

Fortunatamente per i nostri scopi è sufficiente avere un metodo per decidere se una dipendenza funzionale X $\rightarrow Y\in F^+$(cioè alla chiusura di un insieme di dipendenze).
Questo può essere fatto calcolando $X^+$ e verificando se $Y \subseteq X^+$.
Questo perchè ricordando il Lemma 1, $X \to Y \in F^A$ se e solo $Y \subseteq X^+$ e $F^{+}= F^A$

Per il calcolo della chiusura dell’insieme di attributi X, denotata con $X^+$, possiamo usare il seguente algoritmo.

![[AlgoritmoCalcoloX.png|600]]

Il calcolo di $X^+$ è utile in diversi casi:
- verificare le condizioni perchè un insieme di attributi sia chiave di uno schema
- verificare se una decomposizione preserva le dipendenze funzionali dello schema originario

Riga di S: si inseriscono in S i signoli attributi che compongo le parti destre delle dipendenze in F la cui parte sinistra è contenuta in Z.
Da questi poi ne aggiungiamo altri per transitività

la condizione di fermata è quando S è già tutto contenuto in Z

![[EsempioUsoAlgoritmoChiusuraX.png|600]]

**Dimostrazione Teorema Calcolo di $X^+$**
Nel file "Chiusura di un Insieme di Attributi"

**Test di unicità della chiave**
Dati uno schema di relazione R e un insieme di dipendenze funzionali F, per vedere se c'è un'unica chiave di R c'è un controllo che può essere fatto.

Calcoliamo l'intersezione degli insiemi $X = R-(W-V)$ con $V \to W \in F$
Se l'intersezione di questi insiemi determina tutto R, allora questa intersezione è l'unica chiave di R

_Esempio_
R = ABCDE
$F = \{AB \to C, AC \to B, D \to E\}$

$X_1$ = ABCDE - (C - AB) = ABCDE - C = ABDE
$X_2$ = ABCDE - (B - AC) = ABCDE - B = ACDE
$X_3$ = ABCDE - (E - B) = ABCDE - E = ABCD

Facendo l'intersezione tra $X_{1}, X_2,X_3$ otteniamo AD
Notiamo che la chiusura di AD non determina tutto R, infatti $(AD)^+$ = AD
Quindi capiamo che non esiste un'unica chiave di R, ma ne esistono tante

---
#### Decomposizioni che Preservano le Dipendenze
Uno schema che non è in 3NF può essere decomposto in più modi in un insieme di schemi in 3NF.

Uno schema di relazione solitamente viene decomposto quando:
- non è in 3NF
- si vuole migliorare l'efficienza degli accessi

Uno schema che non è in 3NF può essere decomposto in più modi in un insieme di schemi in 3NF, ma abbiamo visto che quando uno schema viene decomposto, non basta che i sottoschemi siano in 3NF

Per formalizzare il concetto di decomposizione che preserva un insieme di dipendenze funzionali iniziamo con la definizione di decomposizione di uno schema di relazione

**Definizione di Decomposizone di uno Schema di Relazione**
Sia R uno schema di relazione. 
Una _decomposizione_ di R è una famiglia $\rho = \{R_{1}, R_{2},..., R_k\}$ di sottoinsiemi di R che ricopre R $\cup_{i=1}^{k} R_i=R$

In altre parole: se lo schema R è composto da un certo insieme di attributi, decomporlo significa definire dei sottoschemi che contengono ognuno un sottoinsieme degli attributi di R. I sottoschemi possono avere attributi in comune, e la loro unione deve necessariamente contenere tutti gli attributi di R.

>[!Warning]
>Una volta ottenuti i sottoschemi bisogna verificare se queste decomposizioni preservano tutte le dipendenze funzionali e forniscono un join senza perdita

**Definizone di Equivalenza tra due Insiemi di Dipendenze Funzionali**
Due insiemi di dipendenze funzionali F e G sono equivalenti se hanno la stessa chiusura
$F \equiv G \text{ se } F^{+}= G^{+}$

quindi bisogna verificare che $F^{+}\subseteq G^+$ e che $G^{+}\subseteq F^+$

Tuttavia calcolare la chiusura di un insieme di dipendenze funzionali richiede tempo esponenziale. Il seguente lemma ci permette però di verificare l'equivalenza dei due insiemi di dipendenze funzionali in tempo polinomiale

**Lemma 2** _(Con Dim)_
Il Lemma 2 viene anche chiamato _Lemma su chiusure_

Siano F e G due insiemi di dipendenze funzionali. Se $F \subseteq G^+$ allora $F^{+}\subseteq G^+$

_Dimostrazione_
Sia $f \in F^{+}-F$ (cioè una dipendenza in $F^+$ che non compare in $F$)
Per il Teorema $F^{+}= F^A$, $f \in F^+$ è derivabile da F mediante gli assiomi di Armstrong.
Dato che $F \subseteq G^+$ significa che ogni dipendenza in F è già presente all'interno di $G^+$, ma se questo è vero allora ogni dipendenza che può essere dedotta a partire da una dipendenza funzionale in F è già presente all'interno di $G^+$.
Per questo motivo è sufficiente considerare F

**Cosa significa che una decomposizione preserva un insieme di dipendenze funzionali?**
_Definizione_
Sia R uno schema di relazione, F un insieme di dipendenze funzionali su R e $\rho = \{R_{1}, R_{2},..., R_k\}$ una decomposizione di R
Diciamo che $\rho$ preserva F se $F \equiv \cup_{i=1}^{k}\pi_{R_i}(F)$
dove $\pi_{R_{i}}(F) = \{X \rightarrow Y | X \rightarrow Y \in F^{+}\land XY \subseteq R_i\}$

