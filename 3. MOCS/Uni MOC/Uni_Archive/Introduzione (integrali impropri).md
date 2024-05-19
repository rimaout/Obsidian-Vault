---
Created: 2024-05-19
Type: Uni Note
Class:
  - "[[Calcolo Integrale (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Integrali]]"
  - "[[Calcolo Integrale (class)]]"
  - "[[Integrali Impropri]]"
Completed: false
---
---

>[!abstract] Index
>1. [[#Cos'è un Integrale Improprio]]
>2. [[#Integrali di Funzioni Illimitate]]

>[!abstract] Related
>- [[Integrali]]
>- [[Integrali Impropri]]
>- [[Calcolo Integrale (class)]]

---
## Cos'è un Integrale Improprio

>[!info] Integrali Propri
>Gli integrali visti fino ad ora sono **integrali propri**, dove:
>- La zona di integrazione è limitata.
>- La funzione integranda è limitata.
>
>![[Pasted image 20240519175329.png|300]]
>
>Se una di queste due proprietà viene meno allora si parla di **Integrale Improprio**.

---
## Integrali di Funzioni Illimitate

>[!info] Funzione illimitata sull'Estremo Destro
>Sia $f(x): [a,b) \to \mathbb{R}$  continue e illimitata sull'estremo destro (ovvero $\lim_{ x \to b^{-}} f(x)=\pm \infty$)
>- In questo caso di definisce:
>$$
>\int^{b}_{a} f( x ) \ dx  = \lim_{ \epsilon \to 0^{+} } \textcolor{orange}{\boxed{\int_{a}^{b-\epsilon} f( x ) \ dx}}\ \ \ \textcolor{orange}{(\text{Integrale Proprio})}
>$$
>
>![[Pasted image 20240519181844.png|650]]

>[!info] Funzione illimitata sull'Estremo Sinistro
>
>Sia $f(x): (a,b] \to \mathbb{R}$  continue e illimitata sull'estremo sinistro (ovvero $\lim_{ x \to a^{+}} f(x)=\pm \infty$)
>- In questo caso di definisce:
>$$
>\int^{b}_{a} f( x ) \ dx  = \lim_{ \epsilon \to 0^{+} } \textcolor{orange}{\boxed{\int_{a+\epsilon}^{b} f( x ) \ dx}}\ \ \ \textcolor{orange}{(\text{Integrale Proprio})}
>$$
>
>![[Pasted image 20240519184313.png|650]]

>[!danger] Converge, Diverge o Indeterminato
>In entrambi i casi, se il limite:
>- Esiste ed è finito, allora $f( x )$ si dice **integrabile** in $[a,b]$ o che $\int^{b}_{a} f( x ) \, dx$ **converge**.
>- Risulta $\pm \infty$, allora si dice che l'integrale proprio **diverge**.
>- Non esiste, allora si dice che l'integrale improprio è **indeterminato**.

>[!example] Esempio
>$$
>\int_{0}^{4} \frac{1}{2\sqrt{ x }} \ dx = \lim_{ \epsilon \to 0^{+} } \int \frac{1}{2\sqrt{ x }} \ dx = \lim_{ \epsilon \to 0^{+} } \sqrt{ x } \Bigg\vert^{4}_{\epsilon} = \lim_{ \epsilon \to 0^{+} } \bigg(\sqrt{ 4 } - \sqrt{ \epsilon }\bigg) = 2- 0 = 2
>$$

---
## Integrali con zona di integrazione illimitata


>[!info] Zona di integrazione illimitata a destra
>Sia $f:[a,+\infty]\to \mathbb{R}$ una funzione continua:
>- In questo caso si definisce:
>$$
>\int^{+\infty }_{a} f(x) \ dx = \lim_{ M \to +\infty } \int^{M}_{a} f( x ) \ dx 
>$$
>
>![[Pasted image 20240519193128.png|700]]

>[!info] Zona di integrazione illimitata a sinistra
>Sia $f:(-\infty, b)\to \mathbb{R}$ una funzione continua:
>- In questo caso si definisce: 
>$$
>\int^{b}_{-\infty} f(x) \ dx = \lim_{ M \to -\infty } \int^{b}_{M} f( x ) \ dx 
>$$
>
>![[Pasted image 20240519194130.png|650]]

>[!example] Esempio
>$$
>\int_{4}^{+\infty} \frac{1}{x^{2}} \ dx = \lim_{ M \to +\infty } - \frac{1}{x} \Bigg\vert^{M}_{4} = \lim_{ M \to +\infty } \bigg( -\frac{1}{M} + \frac{1}{4}\bigg) = 0+ \frac{1}{4} = \frac{1}{4}
>$$

