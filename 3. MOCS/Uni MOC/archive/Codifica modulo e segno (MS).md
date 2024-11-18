---
created: 2023-10-03
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[Sistema di numerazione binario]]"
completed: true
updated: 2024-11-18T20:21
---
>[!abstract] Index
>1. [[#Definizione]]
>2. [[#Bit di segno]]
>3. [[#Intervalli di rappresentazione]]
>4. [[#Conversione]]

>[!abstract] Related
>- [[Sistema di numerazione binario]]
>- [](Sistema%20di%20numerazione%20binario.md)%20numerici.md)emi Digitali (class)]]

---
## Definizione
La codifica modulo e segno è il metodo più semplice e immediato per la rappresentazione dei numeri con segno in informatica. 

Ma è praticamente inutilizzata nel modo reale infatti:
- Rappresentazione ambigua delle zero (leggi: [[#Intervalli di rappresentazione|doppia rappresentazione dello 0]])
- Operazioni difficili da fare, specialmente per un calcolatore

---
## Bit di segno
Il bit di segno è il bit più a sinistra (bit più significativo) della sequenza binaria di un numero in modulo e segno, questo se è:
- *0* allora il numero è *positivo* 
- *1* allora il numero è *negativo*

>**oss:** La ***rappresentazione minima*** in modulo e segno richiede sempre l'utilizzo di un bit in più rispetto alla rappresentazione in binario puro

$$
\begin{gather}
& \text{Numero di bit necessari per rappresentazione:} \\
& \\
& \textcolor{orange}{[log_{2}N]+1}\\
& \\
&\text{ovvero parte intera superiore di }\log_{2}N +1
\end{gather}
$$

---
## Intervalli di rappresentazione


Con n bit si possono rappresentare numeri nell'intervallo: 

$$ [2^{n-1},\  2^{n-1}]$$

Quindi si possono rappresentare *2^n numeri*, di cui:

$$ 
\begin{align}
& - 2^{n-1}-1 \ \ negativi \\
& - 2^{n-1}-1 \ \ positivi \\
& - due \ \ 0,\text{uno positivo e uno negativo}\end{align}
$$


>[!warning] Osservazione
>- **Doppia rappresentazione dello 0** ovvero lo soro può essere rappresentato sia con il segno positivo sia con il segno negativo
>- **Rappresentazione simmetrica:** Stesso numero di bit sia per i numeri positivi che negativi
 
>**Esempio 8bit:** -127 ~ +127

---
## Conversione 

>[!note] Procedimento 
>1. Convertire b10 -> b2
>2. Aggiungere bit di segno:
>	- 0 se positivo
>	- 1 se negativo

| B10    | B2      | MS         |
| ------ | ------- | ---------- |
| *-*15  | 1111    | *1*1111    |
| *+*23  | 10111   | *0*10111   |
| *-*56  | 111000  | *1*111000  |
| *+*85  | 1010101 | *0*1010101 |
| *-*127 | 1111111 | *1*1111111 |


