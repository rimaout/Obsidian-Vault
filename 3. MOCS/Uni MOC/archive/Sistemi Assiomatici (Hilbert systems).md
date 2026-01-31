---
created: 2023-06-11
type: Uni Note
class:
  - "[[Metodi matematici per l'informatica (class)]]"
related:
  - "[[Logica Proposizionale]]"
completed:
updated: 2026-01-31T13:32
---
---
# Definizioni
- [[#Assioma]]
- [[#Sistema Assiomatico]]
- [[#"istanza" di un assioma]]
- [[#Regola di inferenza **Modus Ponens**]]
- [[#Dimostrazioni all'interno di un sistema assiomatico]]
- [[#Teorema in un sistema assiomatico]]
- [[#Derivazione in un sistema assiomatico]]

---
## Assioma
Un **assioma** è una proposizione che si ritiene vera per evidenza, gli vengono utilizzati come fondamenta per costruire teoremi

---
## Sistema Assiomatico
Un **sistema assiomatico** è una famiglia di *assiomi* e delle [[#Regola di inferenza **Modus Ponens**|regole di inferenza]] con cui dedurre nuove formule a partire dagli assiomi

---
## "istanza" di un assioma
Un **"istanza" di un assioma** è una formula che otteniamo sostituendo formule ben formate alle variabili (lettere proposizionali) dell'assioma


***Esempio:***
$$ 
\begin{align} \\
& \text{Assioma : } x\implies (y \implies x)\ \text{ è \ tautologia}\ \  \textcolor{orange}{(0)}\\ \\

& se: \ \ \ x= (p \ \lor \neg p)\\
& \ \ \ \ \ \ \ \ \ \ y= (q \implies(r\implies p) ) \\ \\

& allora: \ (p \ \lor \neg p) \implies ( (q \implies(r\implies p)) \implies (p \ \lor \neg p)) \ \ \ \ \ \ \textcolor{orange}{(1)}\\


\end{align}
$$

**oss:** *(1)* è sempre una tautologia e per dimostralo basta osservare che *(1)* è un istanza dell assioma *(0)*

---
## Regola di inferenza **Modus Ponens**

**Regola:** Se abbiamo la formula X e la formula X-->Y, allora possiamo dedurre la formula Y

**Oss:** se X e X-->Y sono tautologie allora anche Y sarà una tautologia

---
# Dimostrazioni all'interno di un sistema assiomatico
- Sia *S* un sistema assiomatico
- Una dimostrazione in *S* è una sequenza di formule in cui ogni formula o è un istanza di un assioma oppure deriva dalle precedenti formule utilizzando la regola di inferenza

##### Teorema in un sistema assiomatico
un **teorema** in un sistema assiomatico è l'ultima formula di una dimostrazione

***Esempio:***

---
## Derivazione in un sistema assiomatico
- Derivare una formula *F* da un insieme *E* di formule è una sequenza di formule in cui ogni formula è 
	- o un istanza di un assioma 
	- o è una delle formule di *E* 
	- oppure *deriva* dalle precedenti tramite una *regola di inferenza*

**Oss:** Le formule contenute da *E* si chiamano **Ipotesi**

###### Scrittura:
$$ E \vdash_{s}F$$
- **Significato:** Dall' insieme di formule *E* deriva la formula *F* nel sistema *S*