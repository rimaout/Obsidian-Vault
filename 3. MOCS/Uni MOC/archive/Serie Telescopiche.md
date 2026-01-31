---
created: 2024-03-08
type: Uni Note
class:
  - "[[Calcolo Integrale (class)]]"
academic year: 2023/2024
related:
  - "[[Serie Numeriche]]"
completed: true
updated: 2026-01-31T13:32
---
---

>[!info] Index
>1. [[#Introduzione]]
>2. [[#Forma esplicita]]
>3. [[#Serie Telescopica Generale]]
>4. [[#Esempi]]
>	- [[#^4343bf|Serie di mengoli]]
>	- [[#^a681b0|Altri esempi]]

---
## Introduzione 

Le **Serie Telescopiche** sono un tipo di [[Serie Numeriche]] che effettuano la somma degli elementi di Successioni in cui sono perenti ==sia termini positivi che negativi che si "mangiano" a vicenda==, lasciando come risultato la somma di alcune dei termini della successione.

>[!warning] oss
>Le [[Serie Telescopiche]] e le[[Serie Geometriche]] sono tra le poche serie di cui si riesce a calcolare esplicitamente il risultato della somma.

---
## Forma Esplicita

Si dice **Serie Telescopica** una serie del tipo:
$$
\sum^{+\infty }_{n=1}(b_{ n }-b_{ n-k })
$$
oppure
$$
\sum^{+\infty }_{n=m} (b_{ n-k }-b_{ n })
$$

>[!danger] Trovare forma esplicita
>La difficoltà più grande delle serie telescopiche è trovare forma esplicita.
>
>Infatti è possibile trovare serie telescopiche (ovvero serie che si comportano nel modo descritto in [[#Introduzione]]) ma che non sono scritte in [[#Forma Esplicita]].
>
> Vedere [[#Esempi]].

---
## Serie Telescopica Generale

>[!danger] Teorema
>Se 
>- Abbiamo una serie $S_{n}$ telescopica nella [[#Forma Esplicita]]
>
>Allora:
>- Il risultato della somma è uguale a: $S_{n}= b_{1} + b_{2} + \dots + b_{n}$
>- La il carattere della serie $S_{n}$ dipende dal limite della successione $a_{ n }$ ovvero:
>
>$$
>S_{ n } = \begin{cases}
>\text{Converge} &\text{se } \lim_{ n \to + \infty }a_{ n } = \ell \in \mathbb{R} \\
>\text{Diverge a} \pm \infty  &\text{se } \lim_{ n \to + \infty } a_{ n } = \pm \infty \\
>\text{Indeterminato} &\text{se } \lim_{ n \to + \infty } a_{ n } \text{ non esiste}
>\end{cases}
>$$

---
## Esempi

>[!note] Serie di Mengoli
>$$
>S_{ n } = \sum^{+\infty }_{n=1} \frac{1}{n(n+1)} = \frac{1}{n} - \frac{1}{n+1}
>$$
>
>Usando [[#Serie Telescopica Generale|Teorema]]:
>-  $\lim_{ n \to +\infty } \frac{1}{n} = 0$ quindi $S_{ n }$ converge
>
>Infatti: 
>	![[Pasted image 20240315145429.png|800]]
>
> Dove: 
>$$
>\lim_{ n \to +\infty } S_{ n } = \lim_{ n \to +\infty } \left[1- \frac{1}{n+1} \right] = 1
>$$
>Quindi:
>$$
>\text{La serie } \sum_{n=1}^{+\infty } \frac{1}{n(n+1)}\ \text{converge a }1
>$$
^4343bf

>[!note] Serie di cui non so il nome
>$$
>S_{ n } = \sum^{+\infty }_{n=1} \ln\left( 1 + \frac{1}{n} \right)
>$$
>
>Dove $\ln\left( 1 + \frac{1}{n} \right)$ può essere riscritto come:
>$$
>a_{ n } = \ln\left( 1 + \frac{1}{n} \right) =  \ln\left( \frac{1+n}{n} \right) =  \ln(n+1) - \ln(n)
>$$
>
>Usando [[#Serie Telescopica Generale|Teorema]]:
>- $\lim_{ n \to \infty }\ln(n) =+\infty$, quindi $S_{ n }$ diverge
>
>Infatti: 
>	![[Pasted image 20240322114809.png|800]]
>
>Dove:
>$$
>\lim_{ n \to +\infty } S_{n} = \lim_{ n \to +\infty } \big[\ln(n+1)\big] = +\infty 
>$$
>
>Quindi:
>$$
>\text{La serie } \sum^{+\infty }_{n=1} \ln(1+n)\ \text{diverge a }+\infty 
>$$
^a681b0
