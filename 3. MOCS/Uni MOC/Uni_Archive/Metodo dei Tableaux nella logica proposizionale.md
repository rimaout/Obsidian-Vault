---
Created: 2023-06-10
Type: Uni Note
Class:
  - "[[Metodi matematici per l'informatica (class)]]"
Related:
  - "[[Logica Proposizionale]]"
Completed: true
---
---
# Indice:
1. [[#Obbiettivo]]
2. [[#Metodo]]
3. [[#Sviluppare una formula]]
4. [[#α o β]]
5. [[#Chiudere una ramo]]
6. [[#Consigli]]

---
## Obbiettivo 
Il metodo dei tableaux è un metodo dimostrativo utilizzato per verificare se una determinata formula è una [[Logica Proposizionale#Tautologie, contraddizioni, contingenze|tautologia]].

---
## Metodo 
Per dimostrare che una determinata formula (*F*) è una tautologia dobbiamo vedere se non esiste alcuna [[Logica Proposizionale#Interpretazioni|interpretazione]] che rendere vera la negazione della formula (*¬F*)

1. Negare *F*
2. Sviluppare *¬F*
3. Continuare a [[#Sviluppare una formula|sviluppare]] le semplificazioni (sotto formule) di *¬F*
...
4. Fermarsi quando si è raggiunta la semplificazione massima ho si è riuscito a [[#Chiudere una ramo|chiudere tutti i rami]]

**Fine:** 
- Se **non è** stato possibile chiudere tutti i rami significa che esiste una o più interpretazioni di *¬F* vere quindi *F* non è una tautologia
- Se **è** stato possibile chiudere tutti i rami allora *¬F* è una contraddizione e *F* è una tautologia

---
## Sviluppare una formula
- Sviluppare una formula significa scomporla nelle sotto formule che la compongono
	- *es:* x ∨ y è composta da x e y 

- Lo sviluppo di una formula o sotto formula può dare due risultati: 
	![[Screenshot 2023-07-13 at 11.39.06.png]]
1. Uno **"stack"** , generato da una formula *α* (alpha) composta da *α1* e *α2* (sotto-formule) posizionate una sopra all'altra
	- ***oss:*** una formula α si può anche chiamare "**formula di tipo AND**"
	
2. Un **"Ramo"**, generato da una formula *β* (beta) composta da *β1* e *β2* (sotto-formule) che si dividono in due rami
	- oss: una formula β si può anche chiamare "**formula di tipo OR**"

---
## α o β
![[IMG_4FC63CE225AB-1 2.jpeg|900]]

> [!nota]
>$${\displaystyle {\begin{array}{lcl}\neg (A\land B)&=&\neg A\lor \neg B\\\neg (A\lor B)&=&\neg A\land \neg B\\\neg (\neg A)&=&A\\\neg (A\Rightarrow B)&=&A\land \neg B\\A\Rightarrow B&=&\neg A\lor B\\A\Leftrightarrow B&=&(A\land B)\lor (\neg A\land \neg B)\\\neg (A\Leftrightarrow B)&=&(A\land \neg B)\lor (\neg A\land B)\end{array}}}$$

**oss:** 
$$\begin{align}
& 1)\ \ \ x \implies y \equiv \neg x \lor y\\ \\

& 2)\ \ \ x \iff y\equiv (x \implies y) \land (y \implies x)\\ \\

& 3)\ \ \ x \iff y\equiv  (\neg x \lor y) \land (\neg y \lor x)\\
 
\end{align}$$
---
## Chiudere una ramo
- chiudere un ramo significa non continuare a semplificare (scomporre) un ramo del tableaux perché si è incontrata una contraddizione

***Esempio:***
![[Screenshot 2023-11-21 at 15.23.42.png|700]]

Se si riesce a chiudere tutti i rami allora abbiamo dimostrato che la formula originale è una tautologia

---
## Consigli 
1. Nello svolgimento di un tableaux si ha libertà su quale parte dello stack o quale ramo svolgere prima.
	- Solitamente è più veloce risolvere le formule *α* (AND) rispetto alle formule  *β* (OR), infatti ogni volta che risolviamo una formula *β* (OR) creiamo 2 rami raddoppiando il numero di operazioni necessarie

---