---
Created: 2021-07-27
Type: Uni Note
Class:
  - "[[Metodi matematici per l'informatica (class)]]"
Related:
  - "[[Dimostrazione Matematica]]"
Completed: false
---
---
# Indice
1. [[#Definizione]]
2. [[#Steps]]
3. [[#Esempi]]

---
# Definizione
Per dimostrare “per assurdo” una certa affermazione P, si assume che sia vera la sua negazione ¬P e si cerca di giungere a un “assurdo”. 

L’assurdo può essere di vari tipi: per esempio, assumendo che ¬P sia vera potremmo:
1. Riuscire a dimostrare che ¬P deve essere anche falsa  
2. Trovare un’affermazione Q che risulta sia vera che falsa  
3. Trovare un’affermazione Q che non può essere né vera né falsa  
4. Trovare un’affermazione Q tale che Q è falsa ma anche ¬Q è falsa
5. ...

Facendo ciò e tenendo conto del [[Principio del terzo Escluso]] avremmo dimostrato che la affermazione P è vera

---
# Steps
1. Tesi
2. Neghiamo la tesi
3. Cerchiamo di contraddire la la tesi negata ("cerchiamo l'assurdo")
4. Quindi costatando che la negazione della nostra tesi è un assurdo, vuol dire che abbiamo dimostrato che la nostra tesi iniziale è vera

---
# Esempi:

###### Non esiste numero razionale minimo
**Tesi:** Tra i numeri razionali maggiori di zero non ne esiste uno minimo 
**Negazione:** Esiste un numero *r* che è più piccolo di tutti gli altri numeri razionali

**Ragionamento per arrivare ad una contraddizione:** 
- se divido *r* per 2 ottengo un altro numero razionale $$ 0 < \frac{r}{2} < r $$
- abbiamo ottenuto un assurdo quindi la nostra tesi è vera

###### Non esiste numero primo massimo 
**Tesi:** Tra i numeri primi non ne esiste uno massimo 
**Negazione:** Esiste un numero *k* che è più grande di tutti gli altri numeri primi

**Ragionamento per arrivare ad una contraddizione:** 
- prendiamo la serie di numeri primi che va da 1 a k
	- p = {1, 2, 3, 5, 7, ..., k}
- se moltiplichiamo tutti i numeri della serie e aggiungiamo 1 otteniamo un altro numero primo 
	- M = 1 * 2 * 3 * 5 * 7 * ... * k +1
	- M è primo infatti nessuno dei primi appartenenti alla serie *p* può dividerlo proprio perché abbiamo aggiunto 1 
- inoltre *M* è chiaramente più grande di *k* quindi abbiamo ottenuto un assurdo


###### √2 non è un numero razionale ???????
**Tesi:** La radice quadrata di 2 non è un numero razionale
**Negazione:** La radice di due è un numero razionale

**Ragionamento per arrivare ad una contraddizione:** 
0. Definizione numero razionale: $$ x,y \in \mathbb Z, ~ mcd(x,y)=1~~t.c.~~ k = \frac{x}{y} $$
1.  *oss:* se √2 è un numero razionale allora può essere scritta come una frazione tra due numeri primi tra loro (ovvero numeri che non hanno nessun divisore in comune) $$ \sqrt{2} = \frac{a}{b} ~~~~ con ~ a ~ e ~ b ~ primi ~ tra ~ loro$$
2.  Rimuovo la radice elevando per alla seconda $$ 2 = \frac{a^2}{b^2} $$
3.  Si può anche scrivere come: $$ a^2 = 2b^2 $$
4.  *oss:* 2b^2 è un numero pari ---> a^2 è pari ---> a è pari

5.  a essendo un numero pari lo possiamo scrivere come prodotto di un numero (k) e 2 $$a = 2k \to a^2 = 4k^2$$
6.  Sostituisco alla formula del passaggi 3 il nuovo valore di a^2 $$ 4k^2 = 2b^2  $$
7. Semplifico: $$ b^2 = 2k^2 $$
8. *oss:* 2k^2 è un numero pari ---> b^2 è pari ---> b è pari

9. Quindi a e b sono tutti e due numeri pari 

10. Se riprendiamo la formula iniziale avevamo detto che a e b dovevano essere numeri primi tra loro ma se a e b sono pari vuol dire che hanno 2 come divisore comune quindi abbiamo ottenuto una contraddizione

