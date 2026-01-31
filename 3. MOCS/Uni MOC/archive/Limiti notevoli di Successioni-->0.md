---
created: 2023-10-28
type: Uni Note
class:
  - "[[Calcolo Differenziale (class)]]"
academic year: 2023/2024
related:
  - "[[Limiti]]"
  - "[[Limiti Notevoli]]"
completed: true
updated: 2026-01-31T13:32
---
>[!abstract] Index
>1. [[#Proprietà]]
>2. [[#Teoremi]]

>[!abstract] Related
>- [[Limiti]]
>- [[Calcolo Differenziale (class)]]

---
## Proprietà

>[!note] Proprietà
>$se \ \ \textcolor{orange}{a_{n}\to 0}\ \text{ allora:}$
>1. $e^{a_{n}}-1\to 0$
>2. $\log_{e}(1+a_{n})\to 0$ 
>3. $sin(a_{n})\to 0$
>4. $tg(a_{n})\to 0$
>5. $arcsin(a_{n})\to 0$
>6. $arctg(a_{n})\to 0$
>7. $1-cos(a_{n})\to 0$    *oss:* $cos(a_{n})\to 1$

>[!warning] Quindi
>1. $e^{a_{n}}-1 \backsimeq a_{n}$
>2. $\log_{e}(1+a_{n})\backsimeq a_{n}$ 
>3. $sin(a_{n}) \backsimeq a_{n}$
>4. $tg(a_{n})\backsimeq a_{n}$
>5. $arcsin(a_{n})\backsimeq a_{n}$
>6. $arctg(a_{n})\backsimeq a_{n}$
>7. $1-cos(a_{n})\backsimeq \frac{{a_{n}}^2}{2}$ 
>
>>Se $a_{ n }\to 0$  $\implies$ $\log(1+a_{ n }) = a_{ n }$
>>Se $a_{ n } \to 1$ $\implies$ $\log(a_{ n }) = a_{ n }-1$

---
## Teoremi

>[!warning] Teorama1
>$$\frac{\textcolor{orange}{prop}}{a_{n}}\to 1$$
>Dove: 
>- $a_{n}\to 0$
>- *prop* = una delle 7 [[#Proprietà]] tranne $1-cos(a_{n})$

>[!warning] Teorema2
>$$\frac{{1-\cos(a_{n})}}{a_{n}}\to 0$$
>$$\frac{{1-\cos(a_{n})}}{{a_{n}}^2}\to \frac{1}{2}$$
>Dove: 
>- $a_{n}\to 0$
