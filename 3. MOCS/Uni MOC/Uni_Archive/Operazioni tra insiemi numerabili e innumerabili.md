---
Created: 
Type: Exam Review
Class:
  - "[[Metodi matematici per l'informatica (class)]]"
Academic Year: 2023/2024
Related: 
Completed: false
---
---
N = Numerabile
R = Innumerabile

*oss:* $\emptyset$ non numerabile

**Unione:**
>[!possibile]
>- $N \cup N=N$ 
>- $R \cup R=R$
>- $R\cup N=R$

>[! warning] Impossible
>- $N \cup N=R$ 
>- $R \cup R=N$
>- $R\cup N=N$

**Intersezione:**
- $N \cap N=N$ 
	- soltanto se $N \cap N\not=\emptyset$ --> quindi esiste intersezione numerabile soltanto se i due insiemi hanno almeno un elemento in comune
- $R \cap R=R$
	- soltanto se $R \cap R\not=N$
	- *oss:* l'intersezione tra due insiemi innumerabili (R) può dare come risultato un insieme numerabile (N) *guarda* [[#Esercizi]]
- $R\cap N=R$ 

---
## Esercizi
Per ogni coppia di insiemi A e B si ha che:
$$\begin{align}
& 1. \ \ \ \ A\cap B \text{ è numerabile, se A è numerabile: \textcolor{orange}{Falso}} \\
& \ \ \ \ \ \ \ \ \ \ \ \ \text{se A numerabile e B}=\emptyset \implies A\cap B = \emptyset \\ \\
& 2. \ \ \ \ A\cap B \text{ è numerabile, se A e B sono numerabili: \textcolor{orange}{Falso}} \\
& \ \ \ \ \ \ \ \ \ \ \ \ \text{se A}= \mathbb{N}^+\ e B=\mathbb{N}^- \implies A\cap B = \emptyset \\ \\
& 3. \ \ \ \ A\cap B\ \text{non è numerabile, se A e B non sono numerabili: \textcolor{orange}{Falso}} \\ 
& \ \ \ \ \ \ \ \ \ \ \ \ \text{se A}= \mathbb{N}\cup\mathbb{R}^+\ e B=\mathbb{N}\cup\mathbb{R}^- \implies A\cap B = \mathbb{N} \\ \\
& 4. \ \ \ \ A\cup B\ \text{è numerabile, se A e B sono numerabili: \textcolor{orange}{Falso}} \\ 
& \ \ \ \ \ \ \ \ \ \ \ \ - \text{se A e B sono numerabili allora }\exists fa:\mathbb{N}\to A \text{(biunivoca)}\ e\ \exists fb:\mathbb{N}\to B\text{(biunivoca)} \\
& \ \ \ \ \ \ \ \ \ \ \ \ - \text{allora}\ fa\cup fb\  \text{è numerabile}\\


\end{align}$$

