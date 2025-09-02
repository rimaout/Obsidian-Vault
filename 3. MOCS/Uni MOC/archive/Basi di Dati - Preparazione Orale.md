---
type: Uni Note
class:
  - "[[Basi di Dati 1 (class)]]"
academic year: 2024/2025
related:
completed: false
created: 2025-02-18T16:16
updated: 2025-09-02T12:13
---
>[!note]- Def 1: Dipendenza Funzionale 🟢
>
>Dato uno schema relazionale `R`, una dipendenza funzionale su `R` è una coppia ordinata di sottoinsiemi non vuoti `X` e `Y` di `R`.
>
>Denominata attraverso $X \to Y$, dove:
>- `X` è il determinante
>- `Y` è il determinato

>[!note]- Def 1.1: Soddisfare Dipendenza Funzionale 🟢
>
>Si dice che un istanza `r` di `R` soddisfa la dipendenza funzionale $X \to Y$ se per ogni coppia di tuple `t1` e `t2` abbiamo che:
>
>Se $t_{1}[X] = t_{2}[X]$ allora $t_{1}[Y] = t_{2}[Y]$
>
>**oss:** un istanza di `R` non è un insieme di tuple, può essere vista come una tabella che rappresenta le relazione.

>[!note]- Def 1.2: Istanza Legale 🟢
>
>Dati uno schema relazionale `R` e un insieme di dipendenze funzionali `F`.
>
>Un istanza `r` di `R` si dice legale se soddisfa tutte le dipendenze funzionali in `F`.

>[!note]- Def 1.3: Chiusura 🟢
>
>Dato uno schema relazionale `R` e un insieme di dipendenze funzionali `F` su `R`.
>
>La chiusura di `F` è denotata con $F^{+}$ ed indica l’insieme di dipendenze funzionali che sono soddisfatte da ogni istanza legale di `R`.
>
>***oss:*** $F \subseteq F^{+}$ ($F$ è contenuto da $F^{+}$)

>[!note]- Def 2: Chiave 🟢
>
>Dati un schema relazionale `R` ed un insieme di dipendenze funzionali `F`  su `R`.
>
>Un sottoinsieme `K` di `R` si dice chiave se:
>- $K \to R \in F^{+}$
>- Per ogni sottoinsieme *proprio* `K'` di `k` si ha che $K' \to R \not \in F^{+}$
>  
>

>[!note]- Def 3: Attributo Primo e Super-chiave 🟢
>Dati uno schema relazionale `R` e un insieme di dipendenze funzionali `F`.
>
>- Un attributo `A` di `R` si dice primo se appartiene ad una chiave di `R`.
>- Un sottoinsieme `X` di `R` si dice super-chiave se contiene una chiave di `R` o alternativamente determina tutto `R` (ovvero la sua chiusura è uguale ad `R`)

>[!note]- Def 4: Dipendenze Parziali e Transitive 🟢
>
>Siano `R` uno schema relazionale e `F` un insieme di dipendenze funzionali e una dipendenza $X \to A \in F^{+}$ con $A \not \in X$.
>
>>La dipendenza si dice **parziale** se contemporaneamente:
>>- `A` non è primo
>>- `X` è contenuto propriamente da una chiave (contenuto ma diverso)
>>  
>>![[Pasted image 20250218173714.png]]
>>
>>**oss:** se non ci sono dipendenze parziali allora gli attributi che non fanno parte di una chiave sono determinati direttamente alle chiavi.
>  
>>La dipendenza si dice **transitiva** se contemporaneamente:
>>- `A` non è primo
>>- per ogni chiave `K` si ha che `X` non è contenuto interamente in `K` e a sua volta `X` non contiene `K`, ovvero:
>>	- $X$ non è contenuto in `K`
>>	- e $K - X \not = \emptyset$ (`X` non contiene nessuna chiave)
>>	  
>>![[Pasted image 20250220170956.png]]
>>	  
>>**oss:** Non abbiamo dipendenze transitive se gli attributi che non appartengono alla chiave, dipendono direttamente dalla chiave e non da altri attributi non chiave.

>[!note]- Def 5: Schema in 3NF 🟢
>
>Sia `R` uno schema relazionale e `F` un insieme di dipendenze funzionali su `R`.
>
>`R` è in **3NF** se per ogni dipendenza funzionale $X \to A \in F^{+}$ tale che $A \not \in X$ si ha che:
>- `X` è una superchiave, oppure
>- `A` è primo

>[!note]- Teo 1: 3NF = no parziali e no transitive 🟢
>
>Sia `R` uno schema relazionale e `F` un insieme di dipendenze funzionali su `R`. Lo schema `R` è 3NF (terza forma normale) se e solo se ***non esistono dipendenze parziali o transitive***.
>
>Obbiettivo dimostrare $3NF \iff \text{no parziali e no transitive}$ 
>
>>**Dimostrazione pare SE:** ($3NF \implies \text{no parziali e no transitive}$) 
>>
>>Se lo schema è in 3NF allora per ogni dipendenza $X \to A$ abbiamo che $A$ è primo, oppure $X$ è super chiave:
>>1. Se `A` è primo viene a mancare la condizione per avere dipendenze parziali e transitive
>>2. Se `A` non è primo allora `X` è superchiave, infatti:
>>	- non possiamo avere dipendenze parziali in quanto l'`X` di quest'ultime deve essere contenuto da una chiave.
>>	- non possiamo avere dipendenze transitive in quanto l'`X` di quest'ultime non deve contenere alcuna chiave.
>
>>**Dimostrazione parte SOLO SE:** ($\text{no parziali e no transitive} \implies 3NF$)
>>
>>Se non abbiamo dipendenze parziali o transitive implica che per ogni dipendenza si ha che:
>>- `A` è primo, oppure
>>- `X` superchiave, condizione che falsifica sia:
>>	- parziale, infatti se `X` superchiave allora `X` non è sotto insieme proprio di `K`
>>	- transitiva, infatti se `X` superchiave allora `k - X` è uguale a $\emptyset$
>>
>>Quindi è in 3NF.

>[!note]- Chiusura $F^{A}$ 🟢
>
>Denotiamo con $F^{A}$ l’insieme di dipendenze funzionali definito nel modo seguente:
>- $\text{se}\ f \in F \text{ allora } f \in F^{A}$
>- ***Assioma della Riflessività:*** $\text{se}\ Y \subseteq X \subseteq R \text{ allora } X \to Y \in F^{A}$]
>- ***Assioma dell' Aumento:*** $\text{se}\ X \to Y \in F^{A} \text{ allora } XZ \to  YZ \in F^{A}\ \ \ \ \forall Z \subseteq  R$
>- ***Assioma della Transività:*** $\text{se}\ X \to  Y \in F^{A} \text{ e } Y \to Z \in F^{A} \text{ allora } X \to  Z \in F^{A}$
>
>Gli ultimi tre sono detti assiomi di Armstrong, esistono altre 3 regole che possono essere derivate dagli assiomi di Armstrong che sono utili per determinare da dipendenze di $F^{A}$ altre dipendenze di $F^{A}$:
>- ***Regola dell' Unione:*** Se $X \to Y\in F^{A}$ e $X \to Z \in F^{A}$ allora $X \to YZ \in F^{A}$
>- ***Regola della Decomposizione:*** Se $X \to Y \in F^{A}$ e $Z \subseteq Y$ allora $X \to Z \in F^{A}$
>- ***Regola della Pseudo-Transività:*** Se $X \to Y \in F^{A}$ e $WY \to Z \in F^{A}$ allora $WX \to Z \in F^{A}$
>  
>**oss:** L'insieme $F^{A}$ può essere ottenuto applicando ricorsivamente gli assiomi di Armstrong su l'insieme di dipendenze funzionali $F$.

>[!note]- Teo 2: Regole derivate da Armstrong 🟢
>
>Sia $F$ un insieme di dipendenze funzionali, allora su questo valgono le 3 regole viste precedentemente:
>
>**Dimostrazione:**
>
>***Unione:***
>- Se $X \to Y \in F^{A}$ allora per l’*aumento* si ha che $X \to XY \in F^{A}$. 
>- Analogamente se $X \to Z \in F^{A}$ sempre per aumento si ha che $XY \to YZ \in F^{A}$
>- Quindi dato che abbiamo $X \to XY$; $XY \to YZ \in F^{A}$ per transitività possiamo dire che $X \to YZ\in F^{A}$.
>
>***Decomposizione:***
>- Se $Z \subseteq Y$ allora per *riflessività* si ha che $Y\to Z \in F^{A}$ 
>- Quindi poiché $X\to Y\in F^{A}$ e $Y\to Z \in F^{A}$ per transitività abbiamo che $X \to Z \in F^{A}$.
>
>***Pseudotransitività:***
>- Se $X\to Y \in F^{A}$, per l’*aumento* possiamo dire che $WX \to WY \in F^{A}$ 
>- Quindi poiché $WX\to WY\in F^{A}$ e $WY\to Z\in F^{A}$ per transitività abbiamo che $WX\to Z\in F^{A}$.
>
>>**oss:** le tre regole sono: 
>>- ***Regola dell' Unione:*** Se $X \to Y\in F^{A}$ e $X \to Z \in F^{A}$ allora $X \to YZ \in F^{A}$
>>- ***Regola della Decomposizione:*** Se $X \to Y \in F^{A}$ e $Z \subseteq Y$ allora $X \to Z \in F^{A}$
>>- ***Regola della Pseudo-Transività:*** Se $X \to Y \in F^{A}$ e $WY \to Z \in F^{A}$ allora $WX \to Z \in F^{A}$

>[!note]- Def 6: $X^{+}$ 🟢
>
>Siano `R` uno schema relazionale e `F` un insieme di dipendenze funzionali su `R`.
>
>Dato un sottoinsieme di `R` chiamato `X`. Denominiamo con $X^{+}_{F}$ la chiusura di `X` rispetto `F`, dove:
>
>$$
>X^{+}_{F} = \{ A : X \to A \in F^{A} \}
>$$
>
>Ovvero l'insieme degli attributi determinati da `X`.

>[!note]- Lemma 1 🟢
>
>Siano `R` uno schema relazionale e `F` un insieme di dipendenze funzionali su `R`.
>
>Si ha che $X\to Y \in F^{A}$ **se e solo se** $Y \subseteq X^{+}$
>
>Dobbiamo **dimostrare** che $X\to Y \in F^{A} \iff Y \subseteq X^{+}$.
>
>Sia $Y = A_{1} A_{2} \dots A_{3}$
>
>>**Parte Se** ($X\to Y \in F^{A} \implies Y \subseteq X^{+}$)
>>
>>Poiché $X \to Y \in F^{A}$ per la regola della *decomposizione* abbiamo che per ogni `i` $X \to A_{i}\in F^{A}$
>>
>>Questo significa che ogni $A_{i}$ è presente in $F+$ q che quindi e quindi $Y \subseteq X^{+}$.
>
>
>>**Parte Solo Se** ($Y \subseteq X^{+} \implies X\to Y \in F^{A}$)
>>
>>Dato che $Y \subseteq X^{+}$, per ogni `i` si ha che $X \to A_{i} \in F^{A}$ pertanto per *unione* $X \to Y \in F^{A}$.

^ad6bfd

>[!note]- Teo 3: $F^{+} = F^{A}$ 🟢
>
>Siano `R` uno schema di relazione ed `F` un insieme di dipendenze funzionali su `R`. Si ha $F^{+} = F^{A}$.
>
>Per dimostrare $F^{+} = F^{A}$ dobbiamo dimostrare che $F^{A} \subseteq F^{+}$ e che $F^{+} \subseteq F^{A}$.
>
>---
>
>**Dimostrazione:** $F^{A} \subseteq F^{+}$ 
>
>Per calcolare $F^{A}$ si applicano ricorsivamente gli assiomi di Armstrong, dobbiamo dimostrare che ogni dipendenza funzionale ottenuta applichiamo un assioma di Armstrong sia presente anche in $F^{+}$.
>
>Questo può essere fatto ***per induzione***, dove:
> 
>- `i` è il numero di applicazioni di uno degli assiomi di Armstrong.
>- il *caso base* $i=0$ indica che non abbiamo applicato nessun assioma e che quindi $F^{A}$ contiene soltanto gli elementi in $F$ e banalmente anche $F^{+}$ contiene gli elementi in $F$
>- l'*Ipotesi induttiva* indica che ogni dipendenza funzionale ottenuta a partire da $F$ applicando gli assiomi di Armstrong un numero di volte minore o uguale a `i–1` è in $F^{+}$. Tre casi si possono presentare:
>
>>**1.** $X \to Y$ ottenuta attraverso l'**assioma della riflessività** in tal caso $Y \subseteq X$. 
>>
>>Quindi date due tuple  `t1` e `t2` tali che `t1[X] = t2[X]`, banalmente si ha `t1[Y] = t2[Y]`.
>
>>**2.** $X \to Y$ ottenuta applicando l'**assioma dell'aumento** ad una dipendenza $V \to W \in F^{A}$, dove quindi $X = VZ$ e $Y = WZ$ per qualche $Z\subseteq R$.
>>
>>Sia `r` un istanza di `R` e siano `t1` e `t2` due tuple in `r`tali che `t1​[X] = t2​[X]` (ovvero `t1[VZ] = t2[VZ]`) si avrà che `t1[V] = t2[V]` e `t1[Z] = t2[Z]`.
>>
>>Visto che per ***ipotesi induttiva*** $V \to W \in F^{+}$ allora possiamo dire che `t1[V] = t2[V]` porta ad avere `t1[W] = t2[W]`. Quindi otteniamo che `t1[Y] = T2[Y]` (ovvero  `t1[VZ] = t2[WZ]`).
>
>>**3.** $X \to Y$ ottenuta applicando l'**assioma della transitività** su due dipendenze $X \to Z$ e $Z \to Y$ appartenenti a $F^{A}$:
>>
>>Sia `r` un istanza di `R` e siano `t1` e `t2` due tuple in `r`tali che `t1​[X] = t2​[X]`.
>>
>>Per ***ipotesi induttiva*** le dipendenze  $X \to Z$ e $Z \to Y$ fanno parte di $F^{+}$.
>>
>>Grazie all'ipotesi induttiva si ha che `t1​[X] = t2​[X]` $\implies$ `t1​[Z] = t2​[Z]` e che `t1​[Z] = t2​[Z]` $\implies$ `t1​[Y] = t2​[Y]`.
>>
>>Quindi per transitività $X \to Y \in F^{+}$.
>
>---
>
>**Dimostrazione:** $F^{+} \subseteq F^{A}$
>
>La dimostrazione è divisa in due parti.
>
>>La **prima parte** consiste nel dimostrare che esiste un istanza legale di $R$ di questo tipo:
>>
>>![[Pasted image 20250304115012.png|600]]
>>
>>Sia `r` un istanza legale e supponiamo per assurdo che la dipendenza funzionale $V \to W \in F$ non sia soddisfatta (quindi `r` sarebbe non legale).
>>
>>Questo implica che tutti le dipendenze in $F$ hanno uguali valori in `V` ed hanno diversi valori in `W` ed in particolare che $V \subset X^{+}$ e $W\cap(R-X^{+}) \not = \emptyset$.
>>
>>Poiché $V \subset X^{+}$, per il [[#^ad6bfd|Lemma 1]] otteniamo che $X \to V \in F^{A}$, e visto che $X \to V$ e $V \to X$ fanno parte di $F^{A}$ allora attraverso l'*assioma della transitività* possiamo dire che $X \to W \in F^{A}$.
>>
>>Se applichiamo il [[#^ad6bfd|Lemma 1]] su $X \to W \in F^{A}$ otteniamo che $W \subseteq X^{+}$ che contraddice $V\cap( R-X^{+}) \not = \emptyset$ dimostrando che non esistono dipendenze funzionali in `R` che non soddisfano $V \to W$.
>
>>La **seconda parte** consiste nel dimostrare che se $X \to F \in F^{+} \implies X \to Y \in F^{A}$.
>>
>>Supponiamo che $X \to Y \in F^{+}$
>>
>>Abbiamo mostrato che `r` è un istanza legale che quindi soddisfa tutte le dipendenze di $F^{+}$, compresa $X \to Y$.
>>
>>Poiché $X \subseteq X^{+}$ le due tuple di `r` coincidono su gli attributi `X` 
>>
>>Poiché `r` soddisfa $X \to Y$, allora le due tuple devono coincidere anche sugli attributi di `Y`.
>>
>>Questo implica che $Y \subseteq X^{+}$ e, per il [[#^ad6bfd|Lemma 1]]  otteniamo che $X \to Y \in F^{A}$

^7ae4ca

>[!note]- Algo 1  🟢
>Prende come input uno schema `R`, un insieme `F` di dipendenze su `R` e un sottoinsieme `X` di `R`. Come output fornisce la chiusura di `X` rispetto ad `F` all’interno della variabile `Z`.
>
>![[Pasted image 20250304180030.png|1000]]

>[!note]- Teo 4: Dimostrazione Teo 4 🔴
>
>L'algoritmo 1 calcola correttamente la chiusura di un insieme di attributi $X$ rispetto ad un insieme di dipendenze funzionali $F$.
>
>**Dimostrazione:**
>
>Indichiamo con $Z^{0}$ il valore iniziale di $Z$ (ovvero $Z^{0} = X$) e con $Z^{i}$ ed $S^{i}$, i valori di $Z$ e $S$ alla i-esima iterazione.
>	
>>***oss:*** $Z^{i} \subseteq X^{+}$ per ogni $i$.
>
>L'obbiettivo è dimostrare che esiste un $i$ tale che $A \in Z^{i}$ *se e solo se* $A \in X^{+}$, per fare ciò scomponiamo la dimostrazione in due parti:
>- Dimostrazione di $A \in Z^{i} \implies A \in X^{+}$
>- Dimostrazione di $A \in X^{+} \implies A \in Z^{i}$
>
>---
>
>**Dimostrazione parte:** $A \in Z^{\text{i}} \implies A \in X^{+}$
>
>L’obiettivo è dimostrare per induzione su `i` che $Z^{\text{i}} \subseteq X^{+}$ per ogni `i`, quindi:
>
>***Ipotesi Induttiva:*** $Z^{i} \subseteq X^{+}$ per ogni `i`.
>
>***Base dell'induzione:*** la base è `i = 0`, poiché $X^{(0)} = X$ e $X \subseteq X^{+}$, si ha che $Z^{(0)} \subseteq X^{+}$
>
>***Induzione:*** 
>
>Per ipotesi induttiva $Z^{(\text{i}-1)} \subseteq X^{+}$
>
>Sia `A` un attributo in $Z^{(\text{i})}-Z^{\text{i}-1}$ (ovvero un attributo aggiunto all'iterazione `i`)
>
>Deve esistere una dipendenza $Y \to V \in F$ tale che $Y \subseteq Z^{(\text{i}-1)}$ e $A \in V$.
>
>Per il lemma 1 abbiamo che $X \to Y \in F^{A}$ (visto che $Y \subseteq Z^{(\text{i}-1)} \subseteq X^{+}$)
>
>Poiché $X \to Y \in F^{A}$ e $Y \to V \in F^{A}$, per transitività abbiamo che $X \to V \in F^{A}$, quindi per il lemma 1 $V \subseteq X^{+}$.
>
>Visto che $A \in V$ e $V \subseteq X^{+}$, allora per ogni $A\in Z^{\text{i}}-Z^{\text{i}-1}$ si ha che $A \in X^{+}$, e quindi si conferma l'ipotesi induttiva $Z^{i}\subseteq X^{+}$
>
>---
>
>**Dimostrazione parte:** $A \in X^{+} \implies A \in Z^{i}$
>
>Questa dimostrazione si divide in altre due parti.
>
>>La **prima parte** consiste nel dimostrare che esiste una istanza legale di $R$ di questo tipo:
>>
>>![[Pasted image 20250309173754.png|700]]
>>
>>Sia `r` un istanza legale e supponiamo per assurdo che la dipendenza funzionale $V \to W \in F$ non sia soddisfatta (quindi `r` sarebbe non legale).
>>
>>Questo implica che tutti le dipendenze in $F$ hanno uguali valori in `V` ed hanno diversi valori in `W` ed in particolare che $V \subset X^{+}$ e $W\cap(R-X^{+}) \not = \emptyset$.
>>
>>Poiché $V \subset X^{+}$, per il [[#^ad6bfd|Lemma 1]] otteniamo che $X \to V \in F^{A}$, e visto che $X \to V$ e $V \to X$ fanno parte di $F^{A}$ allora attraverso l'*assioma della transitività* possiamo dire che $X \to W \in F^{A}$.
>>
>>Se applichiamo il [[#^ad6bfd|Lemma 1]] su $X \to W \in F^{A}$ otteniamo che $W \subseteq X^{+}$ che contraddice $V\cap( R-X^{+}) \not = \emptyset$ dimostrando che non esistono dipendenze funzionali in `R` che non soddisfano $V \to W$.

>[!note]- Def 7: Decomposizione 🟢
>
>Sia `R` uno schema di relazione. Una **decomposizione** di `R` è una famiglia $ρ = \{ R_{1}​,\, R_{2}​,\, …,\, R_{k}​\}$ di sottoinsiemi di `R` che ricopre `R`, ovvero tale che $\bigcup^{k}_{i=1} R_{i} = R$.

>[!note]- Def 8: Equivalenza tra insiemi di dipendenze funzionali 🟢
>
>Siano $F$ e $G$ due insiemi di dipendenze funzionali. $F$ e $G$ si dicono equivalenti ($F \equiv G$) se $F^{+} = G^{+}$.
>
>>***oss:*** verificare l'equivalenza richiederebbe tempo esponenziale dato che dovremmo calcolare che $F^{+}$ e anche $G^{+}$, per questo possiamo utilizzare il [[#^fcc7ac|Lemma 2]].

>[!note]- Lemma 2 🟢
>
>Siano $F$ e $G$ due insiemi di dipendenze funzionali, se $F \subseteq G^{+}$ allora $F^{+} \subseteq G^{+}$.
>
>>**Dimostrazione:** Sia $f \in F^{+}-F$, poiché per il [[#^7ae4ca|teorema 3]] `f` è derivabile fa `F` mediante gli assiomi di Armstrong e ogni dipendenza funzionale in `F` è derivabile da `G` mediante gli assiomi di armstrong, `f` è derivabile da `G` mediante gli assiomi di Armstrong.

^fcc7ac

>[!note]- Def 9: Decomposizione preserva F 🟢
>
>Sia $R$ uno schema relazionale ed $F$ un insieme di dipendenze funzionali su $R$.
>
>Definiamo con $\rho = \{ R_{1},\, R_{2},\, \dots ,\, R_{k} \}$ una decomposizione di $R$ (ovvero $R = R_{1} \cup r_{2} \cup \dots \cup R_{k}$)
>
>Questa decomposizione si dice che preserva `R` se $F \equiv \bigcup^{k}_{i=1}\pi_{R_{i}}(F)$, dove:
>
>$$
>\pi R_{i}(F) = \{ X \to  Y:\ \ X \to  Y \in F^{+} \wedge XY \subseteq  R_{i} \}
>$$
>
>>***oss:*** Per verificare l'equivalenza tra $F$ e $G$ , dove $G = \bigcup^{k}_{i=1}\pi_{R_{i}}(F)$, ci basta verificare che $F \subseteq G^{+}$, infatti $G \subseteq ^{+}F$ sappiamo essere vero per definizione.

>[!note]- Algo 2 🟡
>
>![[Pasted image 20250310092640.png|800]]
>
>Questo algoritmo richiede che venga calcolato $X^{+}_{G}$ ma noi non conosciamo $G$ quindi usiamo il prossimo algoritmo per calcolarlo ([[#^c94635|Algo 3]]).

>[!note]- Algo 3 🟡
>
>![[Pasted image 20250310093023.png|850]]

^c94635

>[!note]- Teorema 5 🔴
>
>Sia `R` uno schema relazionale, `F` un insiemi di dipendenze funzionali su `R` e $\rho = \{ R_{1},\, R_{2}, \, \dots, R_{k} \}$ una decomposizione di `R` e `X` un sotto insieme di `R`.
>
>L'algoritmo 3 calcola correttamente $X^{+}_{G}$
>
>---
>
>**Dimostrazione**
>
>Indichiamo con $Z^{(0)}$ il valore iniziale di $Z$ (ovvero $Z^{0} = X$), ed in particolare con $Z^{(\text{i})}$ il valore di $Z$ dopo l'i-esima iterazione dell'assegnazione $Z = Z \cup S$. 
>
>Indichiamo con $Z^{f}$ il valore di $Z$ al termine dell algoritmo.
>
>>***oss:*** $Z^{(\text{i})} \subseteq Z^{(\text{i}+1)}$
>
>
>

>[!note]- Def 10: Join senza perdita 🟢
>
>Sia $R$ uno schema relazionale. Una decomposizione di $\rho$ di $R$ ha un join senza perdita se per ogni istanza legale $r$ di $R$ si ha $r = \pi_{R_{i}}(r) \bowtie \dots \bowtie \pi_{R_{k}}(r)$

>[!note] Teorema 6 🟢
>
>Sia $R$ uno schema relazionale e $\rho$ una decomposizione di $R$.
>
>Per ogni istanza di $R$, indichiamo con $m_{\rho}(r) = \pi_{R_{1}}(r) \bowtie \dots \bowtie \pi_{R_{k}}(r)$ che ha queste 3 proprietà:
>
>1. $r \subseteq m_{p}(r)$, indica che il risultato del join potrebbe avere introdotto nuove tuple nelle tabella, portando a una *perdita di informazioni*. Il join si dice senza perdita se $r = m_{\rho}(r)$.
>2. $\pi_{R_{i}}(m_{\rho}​(r)) = \pi_{R_{i}​}(r)\ \text{ per ogni }\, i$, indica che se facciamo la proiezione di qualsiasi schema $R_{i}$ della decomposizione sul join, otteniamo lo stesso se effettuiamo la stessa proiezione sullo istanza originale `r`.
>3. $m_{\rho}(m_{\rho}(r)) = m_{\rho}(r)$ 

>[!note] Algo 4: Tabella 🔴

>[!note] Teorema 4: Dimostrazione Tabella 🔴

>[!note] Def 11: Copertura minimale 🟢
>
>Sia `F` un insieme di dipendenze funzionali, una **copertura minimale** di `F` è un insieme `G` di dipendenze funzionali equivalente ad `F`  tale che:
>1. Ogni dipendenza in `G` ha la *parte destra singleton*
>2. Per nessuna dipendenza $X \to A\in G$ esiste un $X' \subseteq X$ tale che $G \equiv G - \{ X \to A \} \cup \{ X' \to A \}$
>3. Per nessuna dipendenza $X\to A \in G$ deve accadere $G \equiv G−\{X\to A\}$.
>
>Ovvero:
>- (1) Si capisce daii
>- (2) *Gli attributi a sinistra non devono essere ridondanti* non devono esistere dipendenze funzionali in `G` tali che se sostituiamo il determinante con un suo sotto insieme `G` rimane equivalente a prima.
>- (3) *Le dipendenze funzionali non devono essere ridondanti* ovvero non deve esistere una dipendenza in `G` che se rimossa `G` rimane quivalente `

>[!note] Algo 5:
>
>

>[!note] Teorema 8

- Quando Istanza legale? ->vuota solo elemento o rispetta definizione
- Algoritmi degli esercizi visti allo scritto
- definire chiusura di F
- Cosa troviamo in  F^+
- Quali sono gli assiomi di Armstrong
- Quando una funzione di hash è buona
- Cosa'è una dipendenza banale
- Definizione di 3NF (fai attenzione a $A \not \in X$)
- Calcolare costo di ricerca medio su file hash, se ho due tabelle diverse la ricerca media vale sempre n/2
- Protocollo a due fasi (concorrenza)
- Quali sono i vantaggi dei due fasi (è serializzabile + dimostrazione)
- Quando uno scheduler è serializabile
- Quando uno scheduler è seriale
- Qual'è il metodo di controllo per vedere che uno scheduler è serializzabile
- Time stamps

Dimostrare la algoritmo della validità della chiusura di $X$ (ovvero $X^{+}$)

