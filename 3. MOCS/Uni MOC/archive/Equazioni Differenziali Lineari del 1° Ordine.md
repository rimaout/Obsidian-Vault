---
created: 2024-05-23
type: Uni Note
class:
  - "[[Calcolo Integrale (class)]]"
academic year: 2023/2024
related:
  - "[[Equazioni Differenziali]]"
completed: true
updated: 2024-05-27T13:29
---
---

>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Esempi]]

>[!abstract] Related
>- [[Equazioni Differenziali]]
>- [[Calcolo Integrale (class)]]

---
## Introduzione

>[!note] Forma
>Le **equazioni differenziali lineari del 1° ordine** sono equazioni lineari che si presentano nella forma:
>$$
>y'(x)+a(x)\cdot y(x)=f(x)
>$$
>Dove:
>- se $a(x) = 0$ allora è un [[Equazioni Differenziali Elementari + Problemi di Cauchy|equazioni differenziali elementare]].
>- se $f(x)= 0$ allora è un [[Equazioni Differenziali a Variabili Separabili|equazione differenziale a variabili separabili]].

>[!note] Metodo Risolutivo
>
>**Eq. differenziale di partenza:**
>$$
>y'(x)+a(x)\cdot y(x)=f(x)
>$$
>
>**Step risoluzione:**
>$$
>\begin{align*}
>& 1)\ \ \ \text{Trovare una primitiva di } a(x)\ \text{ (cioè una funzione } A(x) \text{ tale che A'(x) = a(x))}\\ \\
>&2)\ \ \ \text{Moltiplicare entrambi i membri per } e^{A(x)}\text{:}\\ \\
>&\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ y'(x)\cdot\textcolor{orange}{e^{A(x)}}+a(x)\cdot y(x)\cdot \textcolor{orange}{e^{A(x)}} = f( x )\cdot \textcolor{orange}{e^{A(x)}}\\ \\
>&3)\ \ \ \text{Integrare entrambi i mebri:}\\ \\
>&\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ y(x)\cdot e^{A(x)} = \int f(x)\cdot e^{A(x)} \, dx+c\\ \\
>&4)\ \ \ \text{Ricavare } y(x) \text{ moltiplicando entrambi i membri per } e^{-A(x)} \text{:}\\ \\
>&\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ y(x) = \textcolor{orange}{e^{-A(x)}}\int f(x)\cdot e^{A(x)} \, dx+c\cdot \textcolor{orange}{e^{-A(x)}}
>\end{align*}
>$$

>[!warning] oss
>$$
>y'(x)\cdot \textcolor{orange}{e^{A(x)}}+ a(x)\cdot \textcolor{orange}{e^{A(x)}}\cdot y(x) = \bigg[ y(x)\cdot e^{A(x)}\bigg]' \implies \int y'(x)\cdot \textcolor{orange}{e^{A(x)}}+ a(x)\cdot \textcolor{orange}{e^{A(x)}}\cdot y(x) \, dx = y(x)\cdot e^{A(x)}
>$$

^41116d

>[!warning] Metodo del Fattore Integrale
>Esistono più metodi per risolvere le equazioni differenziali lineari del 1° ordine, il [[#^41116d|metodo appena citato]] è chiamato **Metodo del Fattore Integranle**.

---
## Esempi

>[!note] Esempio
>![[Pasted image 20240526213718.png|700]]

