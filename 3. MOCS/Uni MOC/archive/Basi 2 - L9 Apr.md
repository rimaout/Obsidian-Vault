---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-04-09T13:53
updated: 2025-04-09T14:43
---

## Alfabeto

## Linguaggio dei Termini

L’insieme dei termini è definito induttivamente come segue:

- ogni variabile in $V$ è un termine
- ogni simbolo di costante in $F$ è un termine
- se $f$ è un simbolo di funzione ($f \in F$) di arità `n > 0` e $t_{1},\, \dots,\, t_{n}$ sono termini, allora anche $f(t_{1}, \, \dots, \, t_{n} )$ è un termine.

## Linguaggio delle Formule

L’insieme delle formule è definito induttivamente come segue:

- se $p$ è un simbolo di predicato di arità `n` e $t_{1},...,t_{n}$ sono termini $p(t_{1},...,t_{n})$ è una formula (detta formula atomica)
- se $\phi$ e $\psi$ sono formule, lo sono anche:

![[Pasted image 20250409141720.png|600]]

se $\phi$ è una formula e $X$ è una variabile allora anche $\forall X \phi$ e $\exists X \phi$ sono formule.

Scriveremo `X = Y` invece di $= (X,Y)$ e $X \not= Y$ al posto di$¬(X=Y)$ (a sua volta al posto di $¬=(X,Y)$).

>[!tip]
>
>Per capire se una formula è veramente una formula dobiamo poterla divideire in quantificatore, variabile, formula

>[!note] Interpretazione


## Valutazione

>[!note] Valutazione dei Termini
>
>

>[!note] Valutazione delle Formule
>
>

