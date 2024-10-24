---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2024-10-24T18:09
updated: 2024-10-24T19:01
---
>[!abstract] Index
>1. 

>[!abstract] Related
>- 

>[!danger] TLDR

---
## Definizione

Dato uno schema di relazione $R$, una dipendenza funzionale su $R$ è una coppia ordinata di sottoinsiemi non vuoti $X,Y$ di $R$.

>[!note] Notazione
>
>$$
>X \to  Y
>$$
>
>Si legge: $X$ **determina funzionalmente** $Y$ oppure $Y$ **dipende funzionalmente da** $X$
>
>Dove:
>- X = **Determinante**
>- Y = **Dipendente**

---
## Soddisfare una dipendenza Funzionale

Dati uno schema $R$ e una dipendenza funzionale $X \to Y$ su $R$, 

Un’istanza $r$ di $R$ soddisfa la dipendenza funzionale $X \to Y$ se:

$$
\forall  t_{1}, t_{2} \in r:\ \ t_{1}[X] = t_{2}[X] \implies t_{1}[Y] = t_{2}[Y] 
$$

>**oss:** Se $t_{1}​[X] \not= t_{2}[X]$ allora la dipendenza è comunque **soddisfatta** qualsiasi siano i valori di $t_{1}​[Y]$ e $t_{2}​[Y]$.

---
## Istanza Legale

Dati uno schema di relazione $R$ e un insieme $F$ di dipendenze funzionali, un’istanza di $R$ è legale se [[#Soddisfare una dipendenza Funzionale|soddisfa]] tutte le dipendenze in $F$.

>[!example] Esempio
>**Istanza R:**
>![[Pasted image 20241024185332.png|300]]
>
>**Dipendenza Funzionale:** $F = \{A \to B\}$
>
>L’istanza $R$ soddisfa la tutte dipendenze funzionali $A \to B$  quindi $R$ è un **istanza legale**.

---
