---
Created: 2024-03-08
Type: Uni Note
Class:
  - "[[Calcolo Integrale (class)]]"
Academic Year: 2023/2024
Related: 
Completed: false
---
---

>[!info] Index
>1. [[#Serie Telescopica Generale]]
>2. [[#Esempi]]
>	- [[#^4343bf|Serie di mengoli]]
>	- [[#^a681b0|Altri esempi]]

---
## Serie Telescopica Generale
**Caso generale:
- sia ${b_{n}}$ una successione infinitesima
- sia $a_{ n }:= b_{n}-b_{n+1}$
- Allora:
	- $\sum^{+\infty}_{n=1}a_{ n }=b_{1}$
	- $S_{n} =  a_{1}-a_{ n }$

---
## Esempi

>[!note] Serie di Mengoli
>$$
>S_{ n } = \sum^{+\infty }_{n=1} \frac{1}{n(n+1)} = \frac{1}{n} - \frac{1}{n+1}
>$$
>
>Infatti: 
>![[Pasted image 20240315145429.png|800]]
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
>Infatti: 
^a681b0

---