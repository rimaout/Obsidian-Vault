---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2024-10-16T15:17
updated: 2024-10-23T16:05
---
>[!abstract] Index
>1. 

>[!abstract] Related
>- 

>[!danger] TLDR

---
## Chiusura di un insieme di dipendenze funzionali

Dato uno schema di relazione $R$ e un insieme $F$ di dipendenze funzionali su $R$.

La **chiusura di F** è l'insieme delle dipendenze funzionale che sono soddisfatte da ogni istanza legale di $R$.

>[!note] Notazione
>$$
>F^{+}
>$$

---
## Chiave

Dati uno schema di relazione $R$ e un insieme $F$ di dipendenze funzionali.

In sottoinsieme $K$ di uno schema di relazione $R$ è una **chiave** di R se:

$$
\begin{align*}
&1. \ \ K \to  R \in F^{+} \\
&2. \ \ \not \exists K' \subseteq   K:\ \ K' \to  K \in F^{+}
\end{align*}
$$

>[!warning] Chiave Primaria
>
>lsvnalòzn

---
## Dipendenze Funzionali Banali

Non possono essere non soddisfatte

---
## Dipendenze Funzionali Proprie


---
## Assiomi di Armstrong

Denotiamo con $F^{A}$ l’insieme di dipendenze funzionali
definito nel modo seguente:
$$
\begin{align*}
&-\ \text{se}\ f \in F \text{ allora } f \in F^{A}\\
&-\ \text{se}\ Y \subseteq X \subseteq R \text{ allora } X \to Y \in F^{A}\ \ \ \ \forall Z \subseteq R\ \ \ \ \ \ \ \ \ \ \ \  \ \ \textcolor{orange}{\text{(assioma della riflessività)}}\\
&-\ \text{se}\ X \to Y \in F^{A} \text{ allora } XZ \to  YZ \in F^{A}\ \ \ \ \forall Z \subseteq  R \ \ \ \  \ \ \textcolor{orange}{\text{(assioma aumento)}}\\
&- \ \text{se}\ X \to  Y \in F^{A} \text{ e } Y \to Z \in F^{A} \text{ allora } X \to  Z \in F^{A}\ \ \ \textcolor{orange}{\text{(assioma della transività)}}
\end{align*}
$$
  
  
---
## Regole derivate dagli assiomi
Ecco altre tre regole derivate dagli assiomi di Armstrong, che consentono di derivare
da dipendenze funzionali in $F^{A}$ altre dipendenze funzionali in $F^{A}$.

$$
\begin{align*}
& - \ \ \ \text{Se } X \to  Y \in F^{A}\ \text{ e }\ X \to  Z \in F^{A}\ \text{ allora }\ X \to  YZ \in F^{A} \\
& - \ \ \ \text{Se } X \to  Y \in F^{A}\ \text{ e }\  \\
& - \ \ \ \text{Se } X \to  Y \in F^{A}\ \text{ e }\ 
\end{align*}
$$
>[!warning]- Dimostrazioni
>
>**Dim. Regola Unione:**
>- Regola: $\text{Se } X \to  Y \in F^{A}\ \text{ e }\ X \to  Z \in F^{A}\ \text{ allora }\ X \to  YZ \in F^{A}$
>
>$$
>\begin{align*}
>&\text{se } X \to  Y \in F^{A}\\
>& \text{per l'assioma dell'aumento di ha che:\\
>& XY \to Yz \in F^{A}\\
>&\text{Quindi, poiche }X\to XY\inF^{A}
>\end{align*}
>$$
>
>**Dim. Regola della Decomposizione:**
>- Regola: $jdsc$
>
>
>**Dim. Regola della Pseudotransitività:**
>- Regola: $vjd$
>
>

**Per regola dell'unione:**


**Per regola della decomposizione:**

---
## Chiusura di un insieme di attributi

>[!note] Definizione
>vdbcskjldbvskfbjkbzjl
>
>$$
>X^{+}_{\ F} = \{ A \vert X \to  A \in F^{A} \}
>$$

**oss:** la chiusura di $X$ non può essere mai vuota perché contiene sempre se stesso ($X \subseteq X^{+}_{\ \ F}$)

**oss:** se la chiusura di $X$ contiene tutti gli attributi allora $X$ è una chiave

>[!example] Esempio 1
>
>- $Cod.Fiscale \to Comune$
>- $Comune \to Provincia$
>  
>Quindi indirettamente $Cod.Fiscale \to Provincia$
>
>$$
>(Cod.Fiscale)^{+}_{\ F}\ = \{Cod.Fiscale, Comune, Provincia \}
>$$

>[!example] Esempio 2
>$$
>Auto(modello, marca, cilindrata, colore)
>$$
>
>Dove:
>- $Modello \to Marca$
>- $Modelo \to Colore$
>  
> Quindi
>$$
>\begin{align*}
>& (Modello)^{+}_{\ F} = \{ Modello, Marca, Colore \}\\
>& (Marca)^{+}_{\ F} = \{ Marca \}\\
>& (Cilindrata)^{+}_{\ F} = \{ Cilindrata\}\\
>& (Colore)^{+}_{\ F} = \{ Colore\}\\
>\end{align*}
>$$
>
>**Osservazioni:**
>- non esiste un singolo attributo che può essere una chiave, ma la coppia modello cilindrato è una chiave
>  
>$$
>(Modello, Cilindrata)^{+}_{\ F} = \{ Modello, Marca, Colore, Cilindrata \}\\
>$$
>
>(modello, cilindrata) è la chiave minimale
>Esempio super chiave = (modello, cilindrata , marca) infatti esiste un sotto insieme (modello cilindrata) che è chiave
>
>
>>Chiave minimale = è l'insieme più piccolo di attributi che può essere usato come chiave (non ha elementi superflui)
>
>>Super chiave = chiave che contiene elementi superflui 

---
## Lemma 1

Sia $R$ uno schema di relazione ed $F$ un insieme di dipendenze funzionali su $R$ vkjdnkj njkds.nvdjknb kjs

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
