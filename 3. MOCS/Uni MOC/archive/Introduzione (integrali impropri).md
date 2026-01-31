---
created: 2024-05-19
type: Uni Note
class:
  - "[[Calcolo Integrale (class)]]"
academic year: 2023/2024
related:
  - "[[Integrali]]"
  - "[[Calcolo Integrale (class)]]"
  - "[[Integrali Impropri]]"
completed: true
updated: 2026-01-31T13:32
---
---

>[!abstract] Index
>1. [[#Cos'è un Integrale Improprio]]
>2. [[#Integrali di Funzioni Illimitate]]
>3. [[#Integrali con zona di integrazione illimitata]]
>4. [[#Esempi]]

>[!abstract] Related
>- [[Integrali]]
>- [[Integrali Impropri]]
>- [[Calcolo Integrale (class)]]
>- [[Esercizi Integrali Impropri]]

---
## Cos'è un Integrale Improprio

>[!note] Integrali Propri
>Gli integrali visti fino ad ora sono **integrali propri**, dove:
>- La zona di integrazione è limitata.
>- La funzione integranda è limitata.
>
>![[Pasted image 20240519175329.png|300]]
>
>Se una di queste due proprietà viene meno allora si parla di **Integrale Improprio**.

>[!note] Integrale Improprio
>
>Sia $f(x)$ una funzione di **discontinuità illimitata** nel punto $x=b$, allora:
>
>$$
>\int^{b}_{a} f(x) \ dx = \text{ Non Integrabile Secondo Rienmann}
>$$
>
>Allora, $f(x)$ si dice **integrabile in senso improprio**  in $[a,\, b]$ se l'integrale per $[a, \, b-\epsilon ]$ dove $\epsilon \to 0^{+}$ ammette limite finito:
>
>$$
>\lim_{ \epsilon \to 0^{+} } \int^{b-\epsilon}_{a} f(x) \ dx = \lim_{ \epsilon \to 0^{+} } F(x) \Bigg\vert^{b-\epsilon}_{a} = \ell
>$$
>
>Dove:
>- $\ell$ è un numero finito 
>- $F(x)$ è una [[Primitive|primitiva]] di $f(x)$

---
## Integrali di Funzioni Illimitate

>[!note] Funzione illimitata sull'Estremo Destro
>Sia $f(x): [a,b) \to \mathbb{R}$  continue e illimitata sull'estremo destro (ovvero $\lim_{ x \to b^{-}} f(x)=\pm \infty$)
>- In questo caso di definisce:
>$$
>\int^{b}_{a} f( x ) \ dx  = \lim_{ \epsilon \to 0^{+} } \textcolor{orange}{\boxed{\int_{a}^{b-\epsilon} f( x ) \ dx}}\ \ \ \textcolor{orange}{(\text{Integrale Proprio})}
>$$
>
>![[Pasted image 20240519181844.png|600]]

>[!note] Funzione illimitata sull'Estremo Sinistro
>
>Sia $f(x): (a,b] \to \mathbb{R}$  continue e illimitata sull'estremo sinistro (ovvero $\lim_{ x \to a^{+}} f(x)=\pm \infty$)
>- In questo caso di definisce:
>$$
>\int^{b}_{a} f( x ) \ dx  = \lim_{ \epsilon \to 0^{+} } \textcolor{orange}{\boxed{\int_{a+\epsilon}^{b} f( x ) \ dx}}\ \ \ \textcolor{orange}{(\text{Integrale Proprio})}
>$$
>
>![[Pasted image 20240519184313.png|600]]

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


>[!note] Zona di integrazione illimitata a destra
>Sia $f:[a,+\infty]\to \mathbb{R}$ una funzione continua:
>- In questo caso si definisce:
>$$
>\int^{+\infty }_{a} f(x) \ dx = \lim_{ M \to +\infty } \int^{M}_{a} f( x ) \ dx 
>$$
>
>![[Pasted image 20240519193128.png|600]]

>[!note] Zona di integrazione illimitata a sinistra
>Sia $f:(-\infty, b)\to \mathbb{R}$ una funzione continua:
>- In questo caso si definisce: 
>$$
>\int^{b}_{-\infty} f(x) \ dx = \lim_{ M \to -\infty } \int^{b}_{M} f( x ) \ dx 
>$$
>
>![[Pasted image 20240519194130.png|600]]

>[!example] Esempio
>$$
>\int_{4}^{+\infty} \frac{1}{x^{2}} \ dx = \lim_{ M \to +\infty } - \frac{1}{x} \Bigg\vert^{M}_{4} = \lim_{ M \to +\infty } \bigg( -\frac{1}{M} + \frac{1}{4}\bigg) = 0+ \frac{1}{4} = \frac{1}{4}
>$$

---
## Integrale Improprio con più problemi


Un integrale improprio può essere suddiviso in più problemi da risolvere.

Infatti è molto comune incontrare integrali che hanno entrambi gli estremi degli intervalli divergenti e che allo stesso momento hanno anche la funzione che diverge in determinati punti.

>[!note] Metodo
In questi casi si deve:
>1.  Spezzare l'integrale in più integrali aventi un singolo problema
>2. Risolvere i singoli integrali
>3. Dedurre il comportamento dell'integrale "globale" sommando i risultati dei vari pezzi.

###### Esempi

![[Esercizi Integrali Impropri#^83648c]]

![[Esercizi Integrali Impropri#^9579a8]]