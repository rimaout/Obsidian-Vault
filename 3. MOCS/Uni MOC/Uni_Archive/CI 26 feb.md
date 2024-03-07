---
Created: 2024-02-26
Type: Uni Note
Class:
  - "[[Calcolo Integrale (class)]]"
Academic Year: 2023/2024
Related: 
Completed: false
---
---
## Index
1. [[#Introduzione]]
2. [[#Struttura esoneri]]
3. [[#Programma]]

---
## Introduzione
- Moodle calcolo integrale Posiglione 23/24 canale II
- Esoneri 2 (per passare esame serve passare tutti e due gli esoneri e se non si passa un esonero serve  ridare tutto)
- Scritto va fatto se non si passa un esonero
- orale solo se vuoi (ma senza orale massimo 27 domande più teoriche tipo definizioni)
- Verranno dati esercizi per esercitarsi su e-learning , + 1 ora a settimana di esercitazione

---
## Struttura esoneri
- Riguardano tutto quello che abbiamo fatto prima dell'esonero
- Si fanno su e-learning: Domande a crocette, domande a risposta aperta
- Voto finale crocette sbagliate abbassano voto
- Durata un ora e un quarto


---
## Programma
- Serie (Taylor)
- Integrali 
- Equazioni differenziali

---
## Serie

>[!def] Q1
>- $E=\{ x\in\mathbb{R}:\ 1\leq x< 2 \}$ E' un [[Intervalli Insiemi|intervallo]]? *si*
>	- $E = [1,2)$

**Notazione formale:**
- $\{ a_{n} \}_{n\in\mathbb{N}}$ 

$a_{n} = (-1)^{n}$
- è oscillante 

$b_{n} = \frac{(-1)^{n}}{n}$ --> 
- $\lim_{ n \to \infty }b_{n}=0$
- $b_{n}\to 0 \equiv |b_{n}-0|$
- $|b_{n}| = \frac{1}{n}$


**Domande da farsi:**
- è continua?
- è derivabile $\forall x \in \mathbb{R}$?
$$
f(x) = \begin{cases}
x &\text{if }x\geq0  \\
-x &\text{if }x<0
\end{cases}
$$

![[Pasted image 20240226100128.png|300]]

$$
\begin{align}
& \lim_{ x \to 0^{+} } \frac{f(x)-f(0)}{x} = \lim_{ n \to 0^{+} } \frac{x-0}{x}=1 \\
& \lim_{ x \to 0^{-} } \frac{f(x)-f(0)}{x} = \lim_{ n \to 0^{-} } \frac{-x-0}{x}=-1 
\end{align}
$$

## Successioni Numeriche


>[!def] Somme Finite
>$$\sum_{k=1}^{100} a_{k} = a_{1}+a_{2}+\dots+a_{100}$$
>$$\sum_{k=1}^{n} a_{k} = a_{1}+a_{2}+\dots+a_{n}$$
>

>[!def] Somme Infinite
>$$\sum_{k=1}^{+\infty } a_{k} $$
>**Caso particolare:**
>se $a_{k}=(-1)^{n}$
>allora $\sum_{k=1}^{+\infty } a_{k} = -1+1-1+1-1+1\dots$ 
>Due possibili risultati:
>- 0
>- -1

>[!def] Somme parziali
>Data $\{ a_{k} \}_{k\in \mathbb{N}}$ poniamo $S_{n} = \sum_{k=1}^{n}a_{k}$

>[!def] Definizione di serie
>- Data: $$\{ a_{n} \}_{n\in \mathbb{N}}$$ 
>- Poniamo:  $$\sum_{k=1}^{+\infty}a_{k}=\lim_{ n \to \infty }S_{n}=\lim_{ n \to \infty } \sum_{k=1}^{n}a_{k}\ \text{ se tale limite esiste}$$

**Scrivere definizione a parole:**


- Se $\lim_{ n \to \infty }S_{n}=S\in \mathbb{R}$
	- se limite esiste ed è finito allora la serie $\sum^{+\infty}_{n=1}a_{n}$ si dice convergente

- Se $S_{n} \to \pm \infty$
	- la serie diverge a $\pm \infty$
	- $\sum^{+\infty}_{n=0}a_{n}=S$

- Se $S_{n}$ oscilla allora
	- $\sum^{+\infty}_{n=1}a_{n}$ non è ben definita 
	- oscilla è irregolare 

>[!example] Esempio:
>- $a_{n}=n\ \ \forall n \in \mathbb{N}$
>- $S_{n}=1+2+3+\dots+n=\frac{n(n+1)}{2} \to +\infty$
>- $\lim_{ n \to +\infty }S_{n}=+\infty=\sum^{+\infty}_{n=1}n$

>[!example] Esempio:
>- $a_{n}=-1\ \ \forall n \in \mathbb{N}$
>- $S_{n}=\sum^{n}_{k=1}-1=-1-1-1\dots=-n$
>- $\sum^{+\infty}_{n=1}=\lim_{ n \to +\infty }-n=-\infty$

>[!example] Esempio serie non ben definite
>- $\sum^{+\infty}_{n=1}(-1)^{n}$ non è ben definita 
>$$S_{n}= \begin{cases}
>& -1 & \text{if } n \text{ è dispari} \\
>& 0 & \text{if } n \text{ è pari}
>\end{cases}$$

>[!example] Esempio serie convergente
>- $a_{n}\not=\text{ solo per un numero finito di addenti =}$ 
>- $\sum^{+\infty}_{n=1}a_{n} \text{ converge (è una sommatoria finita)}$

