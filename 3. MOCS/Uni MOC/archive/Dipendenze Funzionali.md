---
type: Uni Note
class:
  - "[[Basi di Dati 1 (class)]]"
academic year: 2024/2025
related: "[[Progettazione basi di dati - Problemi e Vincoli]]"
completed: true
created: 2024-10-24T18:09
updated: 2025-09-26T16:55
---
>[!abstract] Related
>- [[Progettazione basi di dati - Problemi e Vincoli]]
>- [[Calcolare chiusura di un insiemi di dipendenze funzionali]]
>- [[Basi di Dati 1 (class)]]

---
## Definizione di Dipendenza Funzionale

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
>- $X$ = **Determinante**
>- $Y$ = **Dipendente**

^74530a

---
## Soddisfare una Dipendenza Funzionale

Dati uno schema $R$ e una dipendenza funzionale $X \to Y$ su $R$, 

Un’istanza $r$ di $R$ soddisfa la dipendenza funzionale $X \to Y$ se:

$$
\forall  t_{1}, t_{2} \in r:\ \ t_{1}[X] = t_{2}[X] \implies t_{1}[Y] = t_{2}[Y] 
$$

>***oss:*** Se $t_{1}​[X] \not= t_{2}[X]$ allora la dipendenza è comunque **soddisfatta** indipendentemente dai valori di $t_{1}​[Y]$ e $t_{2}​[Y]$.

---
## Istanza Legale

Dati uno schema di relazione $R$ e un insieme $F$ di dipendenze funzionali, un’istanza di $R$ è legale se [[#Soddisfare una dipendenza Funzionale|soddisfa]] tutte le dipendenze in $F$.

>[!example]- Esempio Legale
>
>![[Pasted image 20241024185332.png|300]]
>
>**Dipendenza Funzionale:** $F = \{A \to B,\ B \to C \}$
>
>L’istanza soddisfa la tutte dipendenze funzionali $A \to B$ e $A \to C$ quindi è un **istanza legale**.

>[!example]- Esempio Non Legale
>
>![[Pasted image 20241108180524.png|300]]
>
>**Dipendenza Funzionale:** $F = \{A \to B,\ B \to C \}$
>
>L’istanza soddisfa la tutte dipendenze funzionali $A \to B$ ma non  tutte le $A \to C$ quindi **NON** è un **istanza legale**.

---
## Chiusura di un Insieme di Dipendenze Funzionali

Dato uno schema di relazione $R$ e un insieme $F$ di dipendenze funzionali su $R$ La **chiusura di** $F$ è l’insieme delle dipendenze funzionali che sono soddisfatte da ogni istanza legale di $R$.

In altre parole la chiusura di un insieme di dipendenze funzionali è l'insieme di tutte le dipendenze funzionali che possono essere derivate dalle dipendenze funzionali dell'insieme originale

- **Notazione:** scriviamo $F^{+}$.
- **oss:** $F \subseteq F^{+}.$

>[!example] Esempio
>Se un istanza $R$ è legale sull'insieme di dipendenze funzionali $F = \{ A \to BC \}$
>
>Allora la chiusura di $F$ è: 
>$$
>F^{+} = \{ A \to BC,\ A \to B,\ A \to C \}
>$$

>**Vedi:** [[Calcolare chiusura di un insiemi di dipendenze funzionali]]

---
## Chiave

Dati uno schema di relazione $R$ e un insieme di dipendenze funzionali $F$, un sottoinsieme $K$ di uno schema di relazione $R$ è una **chiave** se rispetta due condizioni:
- **Condizione 1:** $K \to R \in F^{+}$ 
- **Condizione 2:** Non esiste un sottoinsieme proprio $K'$ di $K$ tale che $K' \to R \in F^{+}$

Dove:
- *Condizione 1* intende che $K$ è un insieme di attributi che determina ogni tupla della relazione.
- *Condizione 2* intende che $K$ è minimale, cioè non esiste un sottoinsieme proprio $K$ che determini funzionalmente tutte le altre attributi di R ($k'$ non deve essere una chiave).

>[!warning] Super Chiave
>Se il sottoinsieme $K$ di $R$ rispetta **soltanto** la **1° condizione** allora è detto **super chiave**, ovvero è una *chiave non minimale*.
>
>Quindi una chiava i cui sottoinsiemi sono a loro volta chiavi è detta super chiave.
>
>>**oss:** Una chiave è sempre super chiave, dato che contiene se stessa, ma una super chiave non è detto che sia sempre chiave, ma ne contiene sempre una.

^12345

>[!warning] Chiave Primaria (SQL)
>
>Dati uno schema $R$ e un insieme $F$ di dipendenze funzionali, possono esistere più chiavi, in [[SQL]] una di esse verrà scelta come **chiave primaria**.
>- Una chiave primaria in SQL **non può avere valore nullo**.
>- Di solito si sceglie quella con meno attributi questo perché migliora la velocità di ricerca nella base di dati.

---
## Dipendenze Funzionali Banali

Dati uno schema di relazione $R$ e due sottoinsiemi di $R$ non vuoti $X,Y$.  Se $Y \subseteq X$ allora ogni istanza $r$ di $R$ soddisfa la dipendenza funzionale $X \to Y$.

>[!note] Definizione
>Se $Y \subseteq X$ allora:
>$$
>X \to  Y \in F^{+}
>$$
>
>Una tale dipendenza funzionale è detta **banale**
>
>>[!example]- Esempio
>>Siano $R = \{ ABCD \}$, i sottoinsiemi $X = ABC$ e $Y= AB$ è banale che:
>>$$
>>X \to  Y \ \text{è soddisfatta} 
>>$$
>>
>>![[Pasted image 20241109175709.png|400]]
>>
>>Quindi ad esempio se abbiamo due tuple uguali su $X=ABC$ allora saranno uguali anche su $Y=AB$.

>[!danger] Prop
>Dati uno schema di relazione $R$ e un insieme di dipendenze funzionali $F$ si ha:
>
>$$
>X \to Y \in F^{+} \iff \forall A \in Y (X \to  Y\in F^{+}) 
>$$
>
>Quindi se $A \to BC \in F^{+}$ allora anche $A \to B \in F^{+}$ e $A \to C \in F^{+}$.
