---
created: 2023-05-21
type: Uni Note
class:
  - "[[Calcolo Differenziale (class)]]"
related:
  - "[[Limiti]]"
  - "[[Funzioni Razionali]]"
updated: 2024-05-27T13:29
---
---
# Definizione
Un limite di una funzione razionale non è altro che, un limite di una frazione che presenta al numeratore o al denominatore un incognita

# Indice:
- [[Limiti di Funzioni Razionali#Limite di funzione razionale con x -->xo|# Limite di funzione razionale con x -->xo]]
- [[Limiti di Funzioni Razionali#Limite di funzione razionale con x -->∞|# Limite di funzione razionale con x -->∞]]

---
# Limite di funzione razionale con x -->xo
Un limite di una frazione che presenta al numeratore o al denominatore un incognita che tende ad un valore finito.
$$\lim_{ n \to x_{0} } \frac{N(x)}{D(x)} $$
#### Metodo Risolutivo:
1. Sostituisco le x della funzione con x0
2. Risolvo la funzione 
	- Esisto *4 possibili casistiche*:
		1. [[Limiti di Funzioni Razionali#**Caso1) non si annullano ne il numeratore ne il denominatore:**|non si annullano ne il numeratore ne il denominatore]]
		2. [[Limiti di Funzioni Razionali#**Caso2) si annulla il numeratore ma non il denominatore:**|si annulla il numeratore ma non il denominatore]]
		3. [[Limiti di Funzioni Razionali#**Caso3) si annulla il denominatore ma non il numeratore:**|si annulla il denominatore ma non il numeratore:]]
		4. [[Limiti di Funzioni Razionali#**Caso4) si annulla sia il denominatore sia il numeratore:**|si annulla sia il denominatore sia il numeratore]]
				

###### **Caso1) non si annullano ne il numeratore ne il denominatore:**
- Il limite esiste e la funzione è continua 

Esempio:![[Screenshot 2023-05-21 at 16.45.17.png]]

###### **Caso2) si annulla il numeratore ma non il denominatore:**
- Il limite esiste e la funzione è continua 

Esempio:![[Screenshot 2023-05-21 at 16.52.07.png]]

###### **Caso3) si annulla il denominatore ma non il numeratore:**
1. Si fa limite destro e sinistro della funzione
		- se limite detestro e sinistro *non congruenti*, il limite non esiste (asintoto verticale) ![[Screenshot 2023-05-21 at 17.09.08.png]]
		- se limite detestro e sinistro *congruenti*, il limite esiste![[Screenshot 2023-05-21 at 17.10.43.png]]

###### **Caso4) si annulla sia il denominatore sia il numeratore:**
- [[Forme Indeterminate dei Limiti|Forma indeteminata]] 0\\0
- Utilizzare metodo scomporre e semplificare![[Screenshot 2023-05-21 at 17.18.36.png]]
---
# Limite di funzione razionale con x -->∞
Un limite di una frazione che presenta al numeratore o al denominatore un incognita che tende ad +- ∞
$$\lim_{ n \to \pm \infty } \frac{N(x)}{D(x)} $$
#### Metodo Risolutivo:
1. Raccogliere il grado massimo al numeratore e al denominatore (come per [[Limiti di Funzioni Polinomiali]])
2. Semplificare 
3. Guardare a cosa tendono i termini superstiti

**Esempi:**![[Screenshot 2023-05-21 at 18.30.07.png]]

**oss:**
- Se *numeratore* è di *grado maggiore* rispetto al denominatore il risultato sarà ∞ 
- Se *numeratore* è di *grado inferiore rispetto* al denominatore il risultato sarà 0
- Se *numeratore* e *denominatore* anno lo *stesso grado* il risultato sarà un numero finito 