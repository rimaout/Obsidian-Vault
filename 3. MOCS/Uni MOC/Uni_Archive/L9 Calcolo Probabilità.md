---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2024-10-16T13:29
updated: 2024-10-16T15:16
---
>[!abstract] Index
>1. 

>[!abstract] Related
>- 

>[!danger] TLDR

---

>[!example] Es Cap 3
>- $D = \# \text{ la persona ha la malattia}$
>- $E = \# \text{ la persona testata è positiva al test}$
>  
>Dove:
>- $P(D \vert E) = 0.95$
>- $P(E\vert D^{c}) = 0.01$
>- $P(D) = 0.005$
>
>Calcolare $P(D\vert E)$ ovvero probabilità che il test risulti positivo quando la persona è malata:
>
>$$
>P(D\vert E) = \frac{P(D \cap  E)}{P(E)} = \frac{P(D) \cdot  P(E \vert D)}{P(D) \cdot  P(E \vert D) + P(D^{c}) \cdot  P(E \vert E^{C})} = \frac{0,005\cdot  0.95}{0.005 \cdot  0.99 + 0.995 \cdot  0,001} = 0,323
>$$

>[!note] Rapporto a favore
>
>Il rapporto a favore di un evento A è definito come:
>
>$$
> \frac{P(A)}{P(A^{c})} = \frac{P(A)}{1 - P(A)}
>$$
>

>[!example] Example
>Partita di calcio Italia Brasile
>
>vl-ndflnkj nkjsndfvjk

---

Consideriamo un ipotesi $H$ (mario rossi è l’assassino) 

Abbiamo una stima di P(H)
Viene introdotto una nuova prova e conoscento E ora la mia stima che H sia vera è $P(H \vert E)$

Come cambia il rapporto a favore dell'evento $H$ con l'introduzione della nuova prova?
Il nuovo rapporto, sapendo $E$, è dato da:
$$
\frac{P(H\vert E)}{P(H^{c}\vert E)}
$$

prima il rapporto favorevole di $H$ era: $\frac{P(H)}{P(H^{c})}$

Provo per il teorema di Bayes:
$$
P(H \vert E) = 
$$

Nuovo rapporto:
$$
\frac{P(H \vert E)}{P(H^{c})\vert E} = \frac{P(H)}{P(H^{c})} \cdot \frac{P\left(  E \vert H  \right)}{P(E^{H^{c}})}
$$


Qui il rapporto favore vole a favore au menta se la nuova prova soddisfa

---

>[!example] Esempio
>
>Un aereo è scomparso e si presumere che possa essere con uguale probabilità in tre possibili zone ($z_{1},z_{2},z_{3}$)
>
>- $1-\beta_{I}$ = è la probabilità di trovare l'aereo nella sona $z_{i}$ se dovesse essere veramente nella sona $z_{i}$
>  
>Sapendo che le ricerche nella zona $z_{1}$ hanno dato esito negativo qual'è la probabilità che l'aereo sia $z_{i}$
>
>- $R_{i}$ = Evento aereo e nella zona $z_{i}$
>  $E$ = Evento la ricerca in $z_{1}$ ha dato esito negativo
>  
> Calcoli:
> 
> $P(z_{1}) = P(z_{2}) = P(z_{3}) = \frac{1}{3}$
> $P(R_{i} \vert E) = \frac{P(E \cap R_{1})}{P(E)} = slajvkjnvkjdnvjk$
> 
> 
> òkvsdhalgvkkhjhskhfj

>[!note] Peoposizione
>Sia $F$ evento con $P(F)>0$, 
>
>Allora la funzione $R \to P(F \vert F)$ , al variare di $E$ eventi, è una funzione di probabilità

>[!warning] Conseguenze
>
>- $P(E^{c}\vert F) = 1- P(E\vert F)$
>- $P(A\cup B \vert F) = P(A\vert F) + P(B\vert F) -  jsvfjkdfjklsbf$

>[!note] Assioma 1
>
>>[!warning]- Dimostrazione

>[!note] Assioma 2
>
>>[!warning]- Dimostrazione
>>

>[!note] Assioma 3
>
>>[!warning]- Dimostrazione

![[Pasted image 20241016145931.png|200]]
