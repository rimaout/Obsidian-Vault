---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-02-18T16:16
updated: 2025-02-18T17:13
---
## Domande


## Preparazione

>[!note]- Def. 1: Dipendenza Funzionale 🟢
>
>Dato uno schema relazionale `R`, una dipendenza funzionale su `R` è una coppia orinata di sottoinsiemi non vuoti `X` e `Y` di `R`.
>
>Denominata attraverso: $X \to Y$.

>[!note]- Def. 1.1: Soddisfare Dipendenza Funzionale 🟢
>
>Si dice che un istanza `r` di `R` soddisfa la dipendenza funzionale $X \to Y$ se per ogni coppia di tuple `t1` e `t2` abbiamo che:
>
>- Se $t_{1}[X] = t_{2}[X]$ allora $t_{1}[Y] = t_{2}[Y]$

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
>

>[!note]- Def. 3: Primo e Super-chiave 🟢
>Dati uno schema relazionale `R` e un insieme di dipendenze funzionali `F`.
>
>- Un attributo `A` di `R` si dice primo se appartiene ad una chiave di `R`.
>- Un sottoinsieme `X` di `R` si dice super-chiave se contiene una chiave di `R` o alternativamente contiene determina tutto `R` (ovvero la sua chiusura è uguale ad `R`)

>[!note]- Def. 4: Dipendenze Parziali e Transitive
>
>Siano `R` uno schema relazionale e `F` un insieme di dipendenze funzionali.

>[!note]- Def. 5: Schema in 3NF 🟢
>
>Sia `R` uno schema relazionale e `F` un insieme di dipendenze funzionali su `R`.
>
>`R` è in **3NF** se per ogni dipendenza funzionale $X \to A \in F^{+}$ tale che $A \not \in X$ si ha che:
>- `A` è primo, oppure
>- `X` è una superchiave

