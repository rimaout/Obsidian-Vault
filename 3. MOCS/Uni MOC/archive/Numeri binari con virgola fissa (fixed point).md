---
created: 2023-10-03
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[Sistema di numerazione binario]]"
completed: false
updated: 2026-01-31T13:32
---
>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Conversioni]]
>3. [[#Range di rappresentazione]]
>4. [[#Operazioni]]

>[!abstract] Related
>- [[Sistema di numerazione binario]]
>- [[Sistemi numerici]]
>- [[Progettazione Sistemi Digitali (class)]]

---
## Introduzione

Il numero è suddiviso in due parti una intera e una decimale

>[!warning] Vantaggi
>- Rappresentazione relativamente semplice e immediata dei numeri decimali
>- Conversioni semplici

>[!warning] Svantaggi
>- Non è possibile variare il range di rappresentazione una volta scelto

---
## Conversioni

>[!note] Nb10 -> Nb2(fixed point)
>- Convertire *parte intera* con [[Sistema di numerazione binario#Conversioni|metodo standard]].
>- Conversione *parte decimale*:
>	1. moltiplicare per 2 (solo parte decimale)
>	2. ripetere moltiplicazione per 2 con risultato del passaggio 1 (solo parte decimale)
>	3. Iterare fino a quando:
>		- otteniamo zero come parte decimale
>		- o ci riteniamo soddisfatti con l'approssimazione (perdita di precisione)
>	4. la concatenazione delle parti intere delle operazione ottenute sarà la parte decimale di N in b2

>[!note] Nb2(fixed point) -> Nb10
>- Convertire *parte intera* con [[Sistema di numerazione binario#Conversioni|metodo standard]].
>- Convertire parte decimale come [[Sistema di numerazione binario#Conversioni|metodo standard]] ma utilizzando potenze di 2^-n

>[!warning] Esempio
>![[IMG_B6AA9B909888-1.jpeg|800]]

---
## Range di rappresentazione

- Per rappresentare un qualsiasi numero in base 2 si hanno a disposizione un certo numero di bit
- Quando si utilizza metodo fixed point si deve scegliere in anticipo quanti bit dedicare alla parte intera e quanti a quella decimale
	- Bit = n
	- Bit parte intera = k
	- Bit parte decimale = n-k

>[!danger] oss
>- più bit dedicheremo alla parte intera più alto sarà il numero rappresentabile
>- più bit educheremo alla parte decimale più precisa sarà l'approssimazione che potremmo fare

>[!warning] Esempi 16 bit
>- Bit = n = 16
>- Bit parte intera = k = 8
>- Bit parte decimale = n-k = 8
>
>- Bit = n =16
>- Bit parte intera = k = 4
>- Bit parte decimale = n-k = 12

---
## Operazioni

🏗️ -- TO-DO -- 🏗️
