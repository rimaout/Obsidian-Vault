---
created: 2023-09-29
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[Sistemi numerici]]"
completed: true
updated: 2026-01-31T13:32
---
>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Conversioni]]
>3. [[#Esempi]]

>[!abstract] Related
>- [[Sistemi numerici]]
>- [](Sistemi%20numerici.md)emi Digitali (class)]]

---
## Introduzione

- Base: 10
- Simboli: 0, 1 , 2 ,3 , 4, 5, 6, 7, 8 ,9
- [[Sistemi numerici#^d06f90|Sistema Posizionale]] 

---
## Conversioni

>[!note] Conversione base10 --> base b
>
>1. ﻿﻿﻿Dividere il numero `N` (base10) per la base `b`, ottenendo così un **quoziente** e un **resto**.
>2. ﻿﻿﻿Dividere il **quoziente** dell'ultima operazione per `b`, ricavando un nuovo quoziente e un nuovo resto.
>3. ﻿﻿﻿Continuare a dividere i quozienti ottenuti per i fino a quando non si ottiene un quoziente uguale a zero.
>4. ﻿﻿﻿I resti della divisione, scritti in ordine inverso rispetto a come li abbiamo ottenuti, formano le cifre del numero `N` espresso in base `b`.

>[!note] Conversione Base b --> base10
>1. Partendo dalla prima cifra a destra assegniamo la posizione alla cifre che compongono il numero partenza.
>2. ﻿﻿﻿Moltiplichiamo la prima cifra per `b0`, la seconda per `b1`, la terza per `b2`, e cosi via fino ad esaurire tutte le cifre.
>3. ﻿﻿﻿sommando i valori trovati al punto 2 avremo il numero espresso nel sistema di numerazione decimale.

---
## Esempi

**Esempio:** [[Conversioni_sistemi_numerici.pdf]]

![[IMG_3423889ADD85-1.jpeg]]