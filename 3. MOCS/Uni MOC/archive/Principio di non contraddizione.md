---
created: 2023-06-26
type: Uni Note
class:
  - "[[Metodi matematici per l'informatica (class)]]"
related:
  - "[[Logica Proposizionale]]"
  - "[[Principio del terzo Escluso]]"
updated: 2026-01-31T13:32
---
---
## Indice
1. [[#Enunciato]]
2. [[#Connettivi Logici]]
3. [[#Equivalenza con Principio del terzo Escluso]]

---
## Enunciato
 *Il principio di non contraddizione stabilisce che se un affermazione è vera allora la sua negazione non può essere vera*, e vice versa
 
 **In altre parole:** Un affermazione non può essere vera e falsa allo stesso momento
 
**oss:** un affermazione che non rispetta il [[Principio del terzo Escluso]] e il [[Principio di non contraddizione]] si dice [[Paradosso logico]]

---
## Connettivi Logici

Utilizzando connettivi logici:
$$ \vDash \neg(p ~ \land \neg p ) $$

---
## Equivalenza con [[Principio del terzo Escluso]]

Utilizzando demorgan è possibili ottenere la definizione logica del principio del terzo escluso

$$ \begin{align}
& - ~\text{principio di non contraddizione:} \vDash \neg(p ~ \land \neg p )\\
& - ~\text{principio del terzo escluso:} \vDash (p ~ \vee \neg p )\\
\end{align} 
 $$
Utilizzando demorgan: 

$$\neg(p ~ \land \neg p ) \leftrightarrow (p ~ \vee \neg p ) $$
