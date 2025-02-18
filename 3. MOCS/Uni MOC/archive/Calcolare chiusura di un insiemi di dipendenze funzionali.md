---
type: Uni Note
class:
  - "[[Basi di Dati 1 (class)]]"
academic year: 2024/2025
related:
  - "[[Dipendenze Funzionali]]"
completed: true
created: 2024-11-09T18:10
updated: 2025-02-17T18:28
---
>[!abstract] Related
>- [[Dipendenze Funzionali]]
>- [[Basi di Dati 1 (class)]]

---
## Introduzione 

Come abbiamo visto trovare la chiusura di l'insieme di dipendenze funzionali $F^{+}$ non è banale. 

In questa sezione vedremo come calcolare un insieme di dipendenze funzionali $F^{A}$ utilizzando gli assiomi di Armstrong e in fine dimostreremo che $F^{A} = F^{+}$.

---
## Assiomi di Armstrong

Denotiamo con $F^{A}$ l’insieme di dipendenze funzionali definito nel modo seguente:
- $\text{se}\ f \in F \text{ allora } f \in F^{A}$
- $\text{se}\ Y \subseteq X \subseteq R \text{ allora } X \to Y \in F^{A}$ [[#^f10628|(Assioma della Riflessività)]]
- $\text{se}\ X \to Y \in F^{A} \text{ allora } XZ \to  YZ \in F^{A}\ \ \ \ \forall Z \subseteq  R$ [[#^c39ea9|(Assioma dell'Aumento)]]
- $\text{se}\ X \to  Y \in F^{A} \text{ e } Y \to Z \in F^{A} \text{ allora } X \to  Z \in F^{A}$ [[#^b70ded|(Assioma della Transitività)]]

>[!danger] Assioma della Riflessività
>
>Se $Y \subseteq X \subseteq R$ allora $X\to Y \in F^{A}$
>
>>***Esempio:***
>>Supponiamo di avere un insieme di attributi $R = \{Indirizzo, Città, Provincia\}$ e un insieme di dipendenze funzionali $F^{A}$ definito come sopra.
>>
>>Se consideriamo l'insieme $X = \{Indirizzo, Città, Provincia\}$ e l'insieme $Y = \{Città\}$, possiamo vedere che $Y \subseteq X \subseteq R$.
>>
>>Secondo l'assioma della riflessività, questo significa che $X \to Y \in F^{A}$, ovvero $\{Indirizzo, Città, Provincia\} \to \{Città\} \in F^{A}$.
>>
>>Stessa cosa vale per $\{Indirizzo, Città, Provincia\} \to \{Indirizzo\}$ e $\{Indirizzo, Città, Provincia\} \to \{Provincia\}$ 

^f10628

>[!danger] Assioma dell'Aumento
>Se $X\to Y \in F^{A}$ allora $XZ \to YZ \in F^{A}$, per ogni $Z \in R$
>
>>***Esempio:***
>>Supponiamo di avere un insieme di attributi $R = \{Nome, Cognome, Età\}$ e un insieme di dipendenze funzionali $F^{A}$ definito come sopra.
>>
>>Se consideriamo l'insieme $X = \{Nome, Cognome\}$ e l'insieme $Y = \{Nome\}$, possiamo vedere che $X \to Y \in F^{A}$, ovvero $\{Nome, Cognome\} \to \{Nome\} \in F^{A}$.
>>
>>Secondo l'assioma dell'aumento, se aggiungiamo un nuovo attributo $Z = \{Età\}$ a $X$ e $Y$, allora la dipendenza funzionale $\{Nome, Cognome, Età\} \to \{Nome, Età\}$ è anche vera.

^c39ea9

>[!danger] Assioma della Transitività
>Se $X\to Y\in F^{A}$ e $Y \to Z \in F^{A}$ allora $X \to Z \in F^{A}$
>
>>***Esempio***
>>Supponiamo di avere un insieme di attributi $R = \{Nome, Cognome, Indirizzo, Città\}$ e un insieme di dipendenze funzionali $F^{A}$ definito come sopra.
>>
>>Se consideriamo l'insieme $X = \{Nome, Cognome\}$ e l'insieme $Y = \{Indirizzo\}$, possiamo vedere che $X \to Y \in F^{A}$, ovvero $\{Nome, Cognome\} \to \{Indirizzo\} \in F^{A}$.
>>
>>Inoltre, se consideriamo l'insieme $Y = \{Indirizzo\}$ e l'insieme $Z = \{Città\}$, possiamo vedere che $Y \to Z \in F^{A}$, ovvero $\{Indirizzo\} \to \{Città\} \in F^{A}$.
>>
>>Secondo l'assioma della transitività, se $\{Nome, Cognome\} \to \{Indirizzo\}$ e $\{Indirizzo\} \to \{Città\}$, allora $\{Nome, Cognome\} \to \{Città\}$.

^b70ded

### Regole derivate dagli Assiomi

Altre tre regole che sono conseguenza degli assiomi di Armstrong che consentono di derivare da dipendenze funzionali in $F^{A}$ altre dipendenze funzionali in $F^{A}$.

>[!danger] Regola dell'Unione
>Se $X \to Y\in F^{A}$ e $X \to Z \in F^{A}$ allora $X \to YZ \in F^{A}$
>>[!warning]- Dim
>>Se $X \to Y \in F^{A}$ per assioma dell'aumento si ha $X \to XY\in F^{A}$.
>>- oss: $XX \to XY \equiv X \to XY$
>>
>>
>>Analogamente $X \to Z \in F^{A}$ diventa $XY \to YZ\in F^{A}$.
>>
>>Quindi per transitività abbiamo che $X \to YZ\in F^{A}$.

>[!danger] Regola della Decomposizione
> Se $X \to Y \in F^{A}$ e $Z \subseteq Y$ allora $X \to Z \in F^{A}$
> 
>>[!warning]- Dim
>>Se $Z\subseteq Y$ allora per riflessività si ha che $Y \to Z \in F^{A}$.
>>
>>Quindi poiché $X \to Y \in F^{A}$ e $Y \to Z \in F^{A}$ allora per transitività $X \to Z\in F^{A}$

>[!danger] Regola della Pseudo-Transitività 
>Se $X \to Y \in F^{A}$ e $WY \to Z \in F^{A}$ allora $WX \to Z \in F^{A}$
>
>>[!warning]- Dim
>>Se $X \to Y \in F^{A}$ per aumento si ha che $WX \to WY \in F^{A}$.
>>
>>Quindi dato che $WX \to WY\in F^{A}$ e $WY \to Z \in F^{A}$ allora per transitività abbiamo che $WX \to Z \in F^{A}$.

>***Capire cosa significa***
>![[Pasted image 20241112190513.png|450]]

---
## Chiusura di un insieme di attributi

>[!note] Definizione
>Siano: 
>- $R$ uno schema di relazione
>- $F$ un insieme di dipendenze funzionali su $R$
>- $X$ un sottoinsieme di $R$
>  
>La chiusura di $X$ rispetto ad $F$ denotata con $X^{+}_{F}$ è definita come:
>
>$$
>X^{+}_{\ F} = \{ A: X \to  A \in F^{A} \}
>$$
>
>Fanno parte della chiusura tutti gli attributi ($A$) che vengono determinati direttamente da $X$ (dipendenze funzionali in $F$), oppure direttamente (dipendenze funzionali in $F^{A}$). Quindi otteniamo che:
>
>$$
>X \subseteq X^{+}_{F}\ \ \ (\text{riflessività})
>$$
>
>Quindi ogni stanza legale se due tuple sono uguali su $X$ allora sono uguali su tutti gli attributi della chiusura di $X$, ovviamente se $F^{A} = F^{+}$ 
>
>***oss*** la chiusura di $X$ non può essere mai vuota perché sicuramente $X$ determina se stesso ($X \subseteq X^{+}_{ F}$)
>
>>[!example]- Esempio 1
>>- $Cod.Fiscale \to Comune$
>>- $Comune \to Provincia$
>>  
>>Quindi indirettamente $Cod.Fiscale \to Provincia$
>>
>>$$
>>(Cod.Fiscale)^{+}_{\ F}\ = \{Cod.Fiscale, Comune, Provincia \}
>>$$
>
>
>>[!example]- Esempio 2
>>Consideriamo uno schema di relazione `Auto` con quattro attributi:
>>
>>$$
>>Auto(modello, marca, cilindrata, colore)
>>$$
>>
>>Siano date le seguenti dipendenze funzionali:
>>
>>- `Modello → Marca`
>>- `Modello → Colore`
>>
>>**Chiusure degli attributi**
>>
>>Le chiusure degli attributi sono:
>>
>>$$
>>\begin{align*}
>>& (Modello)^{+}_{\ F} = \{ Modello, Marca, Colore \}\\
>>& (Marca)^{+}_{\ F} = \{ Marca \}\\
>>& (Cilindrata)^{+}_{\ F} = \{ Cilindrata\}\\
>>& (Colore)^{+}_{\ F} = \{ Colore\}\\
>>\end{align*}
>>$$
>>
>>**Osservazioni**
>>
>>* Non esiste un singolo attributo che possa essere una chiave.
>>* La coppia `(Modello, Cilindrata)` è una chiave.
>>
>>**Chiusura della coppia (Modello, Cilindrata)**
>>
>>La chiusura della coppia `(Modello, Cilindrata)` è:
>>
>>$$
>>(Modello, Cilindrata)^{+}_{\ F} = \{ Modello, Marca, Colore, Cilindrata \}
>>$$
>>
>>**Chiave minimale e super chiave**
>>
>>* La *chiave minimale* è `(Modello, Cilindrata)`, che è l'insieme più piccolo di attributi che può essere usato come chiave.
>>* Una *super chiave* è `(Modello, Cilindrata, Marca)`, che contiene elementi superflui.

>[!warning] Lemma 1
>
>Siano $R$ uno schema di relazione ed $F$ un insieme di dipendenze funzionali su $R$ si ha che: 
>
>$$
>X \to Y \in F^{A} \text{ se e solo se } Y \subseteq X^{+}
>$$
>
>>[!warning]- Dim
>>Sia $Y = A_{1}, A_{2}, \dots, A_{n}$
>>
>>**Parte Se:**
>>Poiché $Y \subseteq X^{+}$ per ogni $i \in \{ 1, \dots, n \}$, si ha che $X \to A_{i}\in F^{A}$, pertanto per la *regola dell’unione* $X\to Y \in F^{A}$
>>
>>**Parte Se e Solo Se:**
>>Poiché $X\to Y \in F^{A}$ per la regola *della decomposizione* si ha che per ogni $i \in \{ 1,\dots,b \}$, $X \to A_{i} \in \in F^{A}$ cioè $A_{i} ​∈ X^{+}$ per ogni $i \in \{ 1,\dots ,n \}$, e quindi $Y \subseteq X^{+}$

---
## Teorema $F^{A}$ = $F^{+}$

**oss:** $F^{A} = F^{+} \implies F^{A} \subseteq F^{+} \wedge F^{+} \subseteq F^{A}$

>[!warning] Osservazione
>$F^{A} \subseteq F^{+}$
>
>Vuol dire che ...

>[!warning] oss
>$F^{+} \subseteq F^{A}$
>
>Vuol dire che ogni dipendenza 

>[!warning] Dimostrazione
>
>Dimostrazione di $F^{A} \subseteq F^{+}$ (utilizzando metodo induttivo):
>
>**Base:**
>- $i = 0$
>- $x \to y \in F \implies x \to y \in F^{+}\ \ \ \ (\text{Dove F} \subseteq F^{+})$  
>
>**Ipotesi Induttiva:**
>- $i-1$
>- $x \to y \in F^{A} \implies x \to y \in F^{+}$
>
>**Passo Induttivo:**
>- $i$
>- $x \to y \in F^{A}$
>
>in poche parole abbiamo dimostrato che indipendentemente dalla numero di applicazione di Armstrong otteniamo sempre $x \to y \in F^{+}$ è soddisfatta da ogni istanza legale
>
>oss: ( $i$ rappresenta il munero di applicazioni di Armstrong)
>
>1) Riflessiva: 
>	- se $x \to y\in F^{A}$ è ottenuta per proprietà riflessiva $\implies Y \subseteq X$
>	- $\forall r \text{ (legale)}\ \ \ t_{1}[x] = t_{2}[x] \ \ y \subseteq x \implies t_{1}[y] = t_{2}[y] \implies x \to y \in F^{+}$
>2) Aumento:
>	- $x \to y \in F^{A}$ ottenuto per aumento $\implies$ in $i-1$ passi $v \to w \in F^{A} \wedge x = vz \wedge y =wz$
>	- $\forall  r \text{ (legale)}\ \ \ t_{1}[x] = t_{2}[x] \implies t_{1}[vz] = t_{2}[vz] \implies t_{1}[v] = t_{2}[v] \wedge t_{2}[z] = t_{2}[z]$ 
>	- oss: per ipotesi induttiva $t_{1}[v] = t_{2}[v] \implies t_{1}[w] = t_{2}[w] \iff t_{1}[z] = t_{2}[z] \implies t_{1}[vz] = t_{2}[vz] \implies t_{1}[y] = t_{2}[y]$
>3) Transitività:
>	- $x \to y \in F^{A}$ ottenuto per transitività $\implies x \to z \in F^{A} \wedge z \to y \in F^{A}$
>	- $\forall r \text{ (legale)}\ \ \ t_{1}[x] = t_{2}[x] \implies t_{1}[z] = t_{2}[z] \implies t_{1}[y] = t_{2}[y]$

>[!warning] Dimostrazione
>Dimostrazione di $F^{+} \subseteq F^{A}$ (utilizzando metodo induttivo):
>
>$x \to y \in F^{+} \implies x\to y \in F^{A}$
>
>prendiamo un istanza di (almeno) due tuple (un istanza di una tupla è sempre legale)
>
>| x^+ | R - x^+ |
>| --- | --- |
>| 1 1 1 1 | 1 1 1 1 |
>| 1 1 1 1 | 0 0 0 0|
>
>Se $T_{1}[v] \not= t1[v]$ allora $r$ soddisfa la dipendenza
>Se $T_{1}[v] = t_{2}[v]\implies v \subseteq x^{+} \implies v \in F^{A} + \to w \in f \implies x \to w \in F^{A}\implies w\in x^{+}\implies t_{1}[w] = t_{2}[w]$
>
>Prendiamo una qualunque dipendenza $v \to w \in F$
>- se $t_{1}[v] \not = t_{2}[v]\ \ (v \cap R-x^{+}) \not = \emptyset$  allora la dipendenza è soddisfatta
>- se $t_{1}[v] = t_{2}[v] \implies v \subseteq x^{+} \text{ (lemma 1)} \implies x \implies v \in F^{A} + v \to w \in F \implies c \to w \in F^{A}$ (lemma 1 alla rovescia) $\implies w \subseteq x^{+} \implies t_{1}[w] = t_{2}[w]$ e quindi la dipendenza è soddifatta
>
>Quindi abbiamo dimostrato che questa è un istanza legale (ovvero soddisfa $x \to y \in F^{+}$)
>
>Se $t_{1}[x] = t_{2}[x]$ allora $t_{1}[y] = t_{2}[y] \implies y \in X^{+} \implies (\text{lemma 1 alla rovescia})\ \ x \to y \in F^{A}$