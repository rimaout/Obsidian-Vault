---
created: 2023-07-13
type: Uni Note
class:
  - "[[Metodi matematici per l'informatica (class)]]"
related:
  - "[[Logica Proposizionale]]"
completed: true
updated: 2024-05-27T13:29
---
---
# Info
- La **logica del primo ordine**  aggiunge alla [[Logica Proposizionale]] i  *quantificatori Universale* ed *Esistenziale*
- Quest'ultimi ci permettono di formalizzare ragionamenti logici più complessi rispetto a quelli possibili con la [[Logica Proposizionale]]

---
# Indice

- [[#Sintassi]]:
	- [[#**Connettivi **|Connettivi ]]
	- [[#**Variabili Individuali **|Variabili Individuali]]
	- [[#**Lettere Predicative **|Lettere Predicative]]
	- [[#Lettere Funzionali]]
	- [[#**Quantificatori **|Quantificatori]]
	- [[Conseguenza logica]] <--

- [[#Definizioni]]:
	- [[#Termine]]
	- [[#Formula Ben Formata]]
	- [[#Interpretazione]]
	- [[#Modello]]
	- [[#Formula Valida]]
	- [[#Tautologia]]
	- [[#Variabili Libere e Vincolate]]
	- [[#Formule chiuse]]
	- [[#Formula Soddisfacibile]]
	- [[#Insieme Soddisfacibile]]

[[#Extra]]:
- [[Interdipendenza tra quantificatori logici]]
- [[Metodo dei Tableaux nella logica del primo ordine]]

---
# Sintassi

### Connettivi:
-  (¬, ∨, ∧, →, . . . ) 
- Usati anche nella logica proposizionale. [[Connettivi logici|Link]]

---
### Variabili Individuali:
- (x, y, z, . . . oppure x1, x2, x3, ...) 
- Assumono i valori di qualsiasi dominio

---
### Lettere Predicative:
- ( P , Q , R, . . . oppure P1 , P2 , P3, . . . ) 
- Indicano una proprietà 

---
### Lettere Funzionali:
- ( f , g , h, . . . oppure f 1 , f2 , f3, . . . ) 
- Per esempio, f(x1, x 2 ) indicherà una [[Funzioni|funzione]] che mappa una coppia ordinata (x1 , x 2) di elementi del dominio in un altri elementi del dominio f(x 1, x 2).

---
### Quantificatori:
- (∀ e ∃).
- [[Interdipendenza tra quantificatori logici]] 
 
>[!Note:] 
>Si utilizzano anche altri simboli aggiuntivi, come:
>
>**[[Logica Proposizionale#Costanti|Costanti:]]** (a, b, c, . . . oppure a1, a2, a3, . . . ), che servono ad indicare specifici elementi del dominio
>

---
# Definizioni

### Termine
- Le variabili e le costanti sono termini. Se *t1, . . . , t* n sono termini e *f* è una lettera funzionale, allora anche *f(t1, . . . , t n)* è un termine.

---
### Formula Ben Formata
- Se *t1, . . . , tn* sono termini e P è una lettera predicativa, allora *P(t1, . . . , t n)* è una formula ben formata ***(f.b.f.)***

**Proprietà:**
1. Se *F* è una ***f.b.f.***, allora anche *¬F*  è una ***f.b.f.***
2. Se *F* e *G* sono ***f.b.f.*** allora anche *F ◦ G* è una ***f.b.f.***, dove con **◦** abbiamo indicato uno qualunque dei connettivi **∧ , ∨ , → , ≡**.
3. se *F* è una ***f.b.f.*** e **x** è una **variabile**, allora anche *∀xF* e *∃xF* sono ***f.b.f.***
4. Nient’altro è una f.b.f

**oss:** il risultato di una f.b.n. è o T o F

---
### Interpretazione
Interpretare una formula (nella logica del primo ordine) significa:
1. Assegnare un *dominio* alle [[#**Variabili Individuali **|variabili individuali]] 
2. Assegnare delle proprietà o relazioni alle [[#**Lettere Predicative **|lettere predicative]]
3. se presenti assegnare valore alle costanti e assegnare funzioni alle lettere funzionali

**oss:** esistono *infinite interpretazioni* di una formula nella logica del primo ordine

---
### Modello
Un modello è un’interpretazione che rende vera una formula

---
### Formula Valida
Una formula *vera in ogni interpretazione* si dice valida

**oss:** una formula valida è sempre vera ma i sui valori dipendono dal significato dei [[#**Quantificatori **|quantificatori]]

---
### Tautologia
Una tautologia nella logica del primo ordine è un *[[Sistemi Assiomatici (Hilbert systems)#"istanza" di un assioma|istanza]] di una tautologia della logica proposizionale*

**oss:** una tautologia è sempre vera indipendentemente dal significato dei [[#**Quantificatori **|quantificatori]]

**Esempio di formula valida che non è tautologia:**
$$ 
-\ Logica \ \ Primo\ \ Ordine:\ \forall xP(x)\implies \exists xP(x)\ \ \ \textcolor{orange}{(formula\ valida)}
$$
- Per ***trovare l'istanza di questa formula nella logica proposizionale*** dobbiamo considerare gruppi di [[#**Variabili Individuali **|variabili Individuali]], [[#**Lettere Predicative **|lettere Predicative]] e [[#**Quantificatori **|quantificatori]] che sono divisi da [[#**Connettivi **|connettivi ]] come singole [[Logica Proposizionale#Lettere proposizionali|lettere proposizionali]]

- Quindi:$$\begin{align}
& - p = \forall xP(x)  \\
& -  q = \exists xP(x)  \\
\end{align}$$
$$ 
-\ Logica \ \ Proposizionale:\ p\implies q\ \ \ \textcolor{orange}{(non\ \ è \ \ tautologia)}
$$

**Esempio di tautologia in F.O.L. :**
$$ 
-\ Logica \ \ Primo\ \ Ordine:\ \forall xP(x)\implies \Big{[}\ \exists xQ(x) \implies \forall xP(x) \Big]\ \ \ \textcolor{orange}{(formula\ valida)}
$$
- Istanza nella logica proposizionale:
$$ 
-\ Logica \ \ Proposizionale:p \implies \Big{[}\ q \implies p\ \Big]\ \ \ \textcolor{orange}{(Tautologia)}
$$
*oss:* L'istanza nella logica proposizionale è una tautologia quindi la formula nella F.L.O è una tautologia

---
### Variabili Libere e Vincolate
Data una formula *F* e una variabile *x*
- *x* si dice **vincolata** in *f* se sta nel raggio di azione del quantificassero 
- *x* si dice **libera** altrimenti

**Esempi:** 
$$ 
\begin{align}
& 1. \ \ \ \ \forall xP(x,y) \ \ \ dove\ x\ è\ vincolata\ e\ y\ è\ libera \\ \\
& 2. \ \ \ \ \forall xP\exists y(x,y) \ \ \ dove\ x\ e\ y\ sono\ vincolati \\
\end{align}
$$

---
### Formule chiuse
Una formula *f* è **chiusa** se *non ha variabili libere*

**oss:** se *f* è chiusa, allora data una qualsiasi interpretazione di *f*, o è *T* o è *F*

---
### Formula Soddisfacibile
Una formula *f* si dice **soddisfacibile** se esiste almeno un interpretazione di in cui *f* è true

**oss:** questa definizione è uguale alla definizione di formula soddisfacibile nella logica proposizionale, l'unica cosa che cambia è il significato di interpretazione

**Come dimostrare che una formula è soddisfacibile:**
- Basta trovare un interpretazione in cui quella formula è vera

**Come dimostrare che una formula non è soddisfacibile:**
- *nota:* soddisfacibile è una proprietà di tipo esistenziale quindi non basta trovare un contro esempio per dimostrare che una determinata formula non è mai vera

- Quindi per dimostrare che una formula *f* non è soddisfacibile, dobbiamo prendere la negata *¬f* e dimostrare che sia una [[#Formula Valida]]

---
### Insieme Soddisfacibile
Un insieme di formule *S* si dice soddisfacibile se esiste un interpretazione che soddisfa tutte le formule di *S*

**Come dimostrare che un insieme è soddisfacibile:**
- Basta trovare un interpretazione che rende tutte le formule del insieme veritiere

**Come dimostrare che un insieme non è soddisfacibile:**
- Bisogna prendere la formula composta dal AND di tutte le formule presenti nel insieme, negarla r dimostrare che questa formula è valida

---