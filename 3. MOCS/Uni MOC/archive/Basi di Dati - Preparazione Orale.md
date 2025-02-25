---
type: Uni Note
class:
  - "[[Basi di Dati 1 (class)]]"
academic year: 2024/2025
related: 
completed: false
created: 2025-02-18T16:16
updated: 2025-02-24T17:39
---
>[!note]- Def. 1: Dipendenza Funzionale 🟢
>
>Dato uno schema relazionale `R`, una dipendenza funzionale su `R` è una coppia orinata di sottoinsiemi non vuoti `X` e `Y` di `R`.
>
>Denominata attraverso $X \to Y$, dove:
>- `X` è il determinante
>- `Y` è il determinato

>[!note]- Def. 1.1: Soddisfare Dipendenza Funzionale 🟢
>
>Si dice che un istanza `r` di `R` soddisfa la dipendenza funzionale $X \to Y$ se per ogni coppia di tuple `t1` e `t2` abbiamo che:
>
>Se $t_{1}[X] = t_{2}[X]$ allora $t_{1}[Y] = t_{2}[Y]$
>
>**oss:** un istanza di `R` non un insieme di tuple, può essere vista come una tabella che rappresenta le relazione.

>[!note]- Def: 1.2: Istanza Legale 🟢
>
>Dati uno schema relazionale `R` e un insieme di dipendenze funzionali `F`.
>
>Un istanza `r` di `R` si dice legale se soddisfa tutte le dipendenze funzionali in `F`.

>[!note]- 1.3: Chiusura 🟢
>
>Dato uno schema relazionale `R` e un insieme di dipendenze funzionali `F` su `R`.
>
>La chiusura di `F` è denotata con $F^{+}$ ed indica l’insieme che sono soddisfatte da ogni istanza legale di `R`
>
>***oss:*** $F \subseteq F^{+}$ ($F$ è contenuto da $F^{+}$)

>[!note]- Def. 2: Chiave 🟢
>
>Dati un schema relazionale `R` ed un insieme di dipendenze funzionali `F`  su `R`.
>
>Un sottoinsieme `K` di `R` si dice chiave se:
>- $K \to R \in F^{+}$
>- Per ogni sotto insieme `K'` si `k` si ha che $K' \to R \not \in F^{+}$

>[!note]- Def. 3: Attributo Primo e Super-chiave 🟢
>Dati uno schema relazionale `R` e un insieme di dipendenze funzionali `F`.
>
>- Un attributo `A` di `R` si dice primo se appartiene ad una chiave di `R`.
>- Un sottoinsieme `X` di `R` si dice super-chiave se contiene una chiave di `R` o alternativamente contiene determina tutto `R` (ovvero la sua chiusura è uguale ad `R`)

>[!note]- Def. 4: Dipendenze Parziali e Transitive 🟢
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

>[!note]- Def. 5: Schema in 3NF 🟢
>
>Sia `R` uno schema relazionale e `F` un insieme di dipendenze funzionali su `R`.
>
>`R` è in **3NF** se per ogni dipendenza funzionale $X \to A \in F^{+}$ tale che $A \not \in X$ si ha che:
>- `X` è una superchiave, oppure
>- `A` è primo

>[!note]- Teo. 1: 3NF = no parziali e no transitive 🟢
>
>Sia `R` uno schema relazionale e `F` un insieme di dipendenze funzionali su `R`. Lo schema `R` è 3NF (terza forma normale) se e solo se ***non esistono dipendenze parziali o transitive***.
>
>**Dimostrazione pare SE:** Se lo schema è in 3NF allora per ogni dipendenza $X \to A$ abbiamo che $A$ è primo, oppure $X$ è super chiave:
>1. Se `A` è primo viene a mancare la condizione per avere dipendenze parziali e transitive
>2. Se `A` non è primo allora `X` è superchiave, infatti:
>	- non possiamo avere dipendenze parziali in quanto l'`X` di quest'ultime deve essere contenuto da una chiave.
>	- non possiamo avere dipendenze transitive in quanto l'`X` di quest'ultime non deve contenere alcuna chiave.
>
>**Dimostrazione parte SOLO SE:** se non abbiamo dipendenze parziali o transitive implica che tutte le dipendenza $X \to A$ avranno $X$ superchiave.

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

>[!note]- Teo. 2: Regole derivate da Armstrong 🟢
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
