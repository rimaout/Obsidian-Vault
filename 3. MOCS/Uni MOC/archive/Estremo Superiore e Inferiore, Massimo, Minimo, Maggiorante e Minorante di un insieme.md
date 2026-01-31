---
created: 2023-04-19
type: Uni Note
class:
  - "[[Calcolo Differenziale (class)]]"
academic year: 2022/2023
related:
completed: true
updated: 2026-01-31T13:32
---
---
## Intervallo 
- intervallo `I` è un sottoinsieme di `R` (numeri reali) definito da due numeri reali (`x1, x2`) chiamati estremi dell'intervallo.

**Definizione:**
- insieme di tutti i numeri compresi tra `x1` e `x2` dove `x1 < x2`

 **Notazione:**
 ***1)***
$$ 
[x1, x2] := \{ x\subseteq \mathbb{R} ~~ t.c ~~ x1 \leq x \leq x2 \} $$
$$
[x1, x2) := \{ x\subseteq \mathbb{R} ~~ t.c ~~ x1 \leq x < x2 \}
$$
$$
(x1, x2] := \{ x\subseteq \mathbb{R} ~~t.c~~ x1 < x \leq x2 \}$$
$$(x1, x2) := \{ x\subseteq \mathbb{R} ~~t.c~~ x1 < x < x2 \}
$$
***2)***
$$ 
(-\infty, x2) := \{ x\subseteq \mathbb{R} ~~t.c~~ x < x2 \} $$
$$ 
(-\infty, x2] := \{ x\subseteq \mathbb{R} ~~t.c~~ x \leq x2 \} $$
$$ 
(x1, +\infty) := \{ x\subseteq \mathbb{R} ~~t.c~~ x > x1 \} $$
$$ 
[x1, +\infty) := \{ x\subseteq \mathbb{R} ~~t.c~~ x \geq x1 \} $$

***3)***
$$ (-\infty, +\infty) := \mathbb{R}$$
**Intervallo chiuso:** \[x1,x2\]
**Intervallo semi aperto:** \(x1,x2\] o \[x1,x2\)
**Iintervallo aperto:** \(x1,x2\)

---

## Maggiorante e Minorante di un insieme reale
- i numeri reali sono un campo totalmente ordinato per cui è possibile usare gli operatori `<,> <=, >=` per confrontare i numeri.

$$ sia ~~ X\subseteq \mathbb{R} ~~un~~sottoinsieme~~reale$$

**Definizione Maggiorate:**
$$ y \in \mathbb{R} ~~maggiorante~~ di ~~X \Leftrightarrow \forall x \in X ~~ risulta che ~~y\geq x  $$

**Definizione Minorante:**
$$  y \in \mathbb{R} ~~minorante ~~di ~~X \Leftrightarrow \forall x \in X ~~ risulta che ~~y\leq x  $$

**oss:** minoranti e maggioranti non devono necessariamente appartenere all'insieme

###### Esempi: 

![[Screenshot 2023-05-12 at 12.38.29.png]]


---

## Limitato Superiormente o Inferiolmente
$$ sia ~~ X\subseteq \mathbb{R},~~ X\ne0 $$
- `X` si dice **Limitato Superiormente** se possiede almeno un maggiorante 
- `X` si dice **Limitato Inferiormente** se possiede almeno un minorante 

- `X` si dice **Limitato** se è limitato sia superiormente che inferiormente
- `X` si dice **llimitato** se non è limitato ne inferiormente ne superiormente

---

## Estremo Superiore ed Inferiore
$$sia ~~ X\subseteq \mathbb{R} ~~un~~sottoinsieme~~reale$$

- **Estremo superiore:** il minimo (più piccolo) dei maggioranti:
$$ \sup(X)= \min(k \in \mathbb{R}:~k~~maggiorante~~di~~X) $$

- **Estremo inferiore:** il massimo (più grande) dei minoranti:
$$ \inf(X)= \max(k \in \mathbb{R}:~k~~minorante~~di~~X) $$

###### Esempi:
![[Screenshot 2023-05-12 at 12.35.29.png]]

## Massimo e Minimo
- Un `maggiorante` appartente all' insieme di dice **Massimo**:
$$ \max(X)$$

- Un `minorante` appartente all' insieme di dice **Minimo**:
$$ \min(X)$$

**oss:** estremo suepriore e inferiore di un insieme vuoto:
$$ \inf{(\emptyset)=+\infty},~~\sup{(\emptyset)=-\infty}$$

###### Esempi:
1. ﻿﻿﻿Dato l'intervallo (1, 10], risulta che:
	- 1 è l'estremo inferiore ma non il minimo, mentre 10 è l'estremo superiore e il massimo

2.  ﻿﻿﻿Dato l'intervallo (-∞, 10), risulta che:
	- -∞ è l'estremo inferiore (ma non il minimo) e che 10 è l'estremo superiore (ma non il massimo)

3.  ﻿﻿﻿Riguardo all'intervallo IR = (-∞, +∞) risulta che:
	- -∞ è l'estremo inferiore (ma non il minimo) e che +∞ è l'estremo superiore (ma non il massimo)