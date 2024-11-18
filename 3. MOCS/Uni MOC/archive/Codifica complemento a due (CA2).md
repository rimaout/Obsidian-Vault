---
created: 2023-08-01
type: Uni Note
academic year: 2022/2023
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
  - "[[Architettura dei calcolatori (class)]]"
related:
  - "[[Codifica complemento a uno (CA1)]]"
  - "[[Codifica modulo e segno (MS)]]"
  - "[[Sistema di numerazione binario]]"
completed: true
updated: 2024-07-09T11:14
---
>[!abstract] Index
>1. [[#Definizione]]
>2. [[#Bit di segno]]
>3. [[#Intervalli di rappresentazione]]
>4. [[#Conversione (metodo circuitale)]]
>5. [[#Conversione (metodo semplificato)]]
>6. [[#Somma complemento a due]]
>7. [[#Sottrazione complemento a due]]
>8. [[#Casi Particolari con Somma/Sottrazione]]
>9. [[#Estensione rappresentazione utilizzando complemento a due]]
>10. [[#Over-flow e Under-flow con complemento a due]]
>11. [[#Over-flow]]
>12. [[#Under-flow]]

>[!abstract] Related
>- [[Sistema di numerazione binario]]
>- [[Sistemi numerici]]
>- [[Progettazione Sistemi Digitali (class)]]

---
## Introduzione

Il **complemento a due**, o **complemento alla base**, è il metodo più diffuso per la rappresentazione dei numeri con segno in informatica. 

La sua enorme diffusione è data dal fatto che i circuiti di addizione e sottrazione non devono esaminare il segno di un numero rappresentato con questo sistema per determinare quale delle due operazioni sia necessaria, permettendo tecnologie più semplici e con maggiore precisione; si utilizza un solo circuito, il [[Circuiti Aritmetici]], sia per l'addizione che per la sottrazione.


>[!info] Esempio
>![[Pasted image 20240305130955.png|700]]

>[!danger] Vantaggi
>1. Non richiede il controllo del bit di segno per effettuare le operazioni
>2. Esecuzione di operazioni di somma e sottrazione con lo stesso circuito
>3. Calcolo dell'opposto relativamente semplice, leggi:
>	- [[#Conversione (metodo circuitale)]]
>	- [[#Conversione (metodo semplificato)]]

---
## Bit di segno

Il bit di segno è il bit più a sinistra (bit più significativo) della sequenza binaria di un numero a complemento a 2, questo se è:
- *0* allora il numero è *positivo* 
- *1* allora il numero è *negativo*

**oss:** La ***rappresentazione minima*** in complemento a 2 richiede sempre l'utilizzo di un bit in più rispetto alla rappresentazione in binario puro

$$
\begin{gather*}
& \text{Numero di bit necessari per rappresentazione:} \\
& \\
& \textcolor{orange}{[log_{2}N]+1}\\
& \\
&\text{ovvero parte intera superiore di }\log_{2}N +1
\end{gather*} 
$$

>[!warning] Esempio
>![[IMG_0DAC102C11E6-1.jpeg|800]]

---
## Intervalli di rappresentazione 

Con n bit si possono rappresentare numeri nell'intervallo: 

$$ [2^{n-1},\ 0\ , 2^{n-1}-1]$$

Quindi si possono rappresentare *2^n numeri*, di cui:

$$ 
\begin{align*}
& - 2^{n-1} \ \ negativi \\
& - 2^{n-1}-1 \ \ positivi \\
& - uno \ \ 0
\end{align*}
$$

>[!warning] Osservazioni
>1.  è possibile rappresentare un numero in meno positivo rispetto ai negativi perché in realtà la codifica del numero 0 fa parte dei numeri positivi.
>2. Si dice **Rappresentazione asimmetrica**.

---
## Conversione (metodo circuitale)

>[!note] Metodo
>1. Scrivere numero in binario (aggiungendo 0 come bit di segno se non è già esteso)
>2. invertire gli 1 con gli 0 e vice versa
>3. Sommare 1

>[!warning] Esempio
>![[IMG_BF76FCA8B06C-1.jpeg|600]]

---
## Conversione (metodo semplificato)

>[!note] Metodo
>1. Trovare il primo 1 della sequenza binaria (da sinistra verso destra)
>2. Invertire tutti i valori dopo quell'1

>[!warning] Esempio
>![[IMG_Comp2Convertion.jpeg|500]]

---
## Somma complemento a due

>[!note] Metodo
>1. Convertiamo i numeri in binario non tenendo conto del segno
>2. Utilizziamo il complemento a due per per convertire i numeri negativi
>3. Effettuo operazione di somma con il [[Sistema di numerazione binario#Somma in binario e sottrazione|metodo standard per i numeri in base 2]]
>4. Effettuiamo la [[#Conversione (metodo circuitale)|conversione del risultato da complemento a due a decimale]]
>
>>**oss:** se il most significant bit è 1 il numero in base 10 e negativo

>[!warning] Esempio
>![[IMG_Comp2Sum.jpeg|800]]

---
## Sottrazione complemento a due

>[!note] Metodo
>1. Convertiamo i numeri in binario non tenendo conto del segno
>2. Utilizziamo il complemento a due per per convertire i numeri negativi
>3. [[#Conversione (metodo circuitale)|Inverto il segno]] di *n2*:  $\text{dove: }n_{1}-\textcolor{orange}{n_{2}}$
>6. Effettuo operazione di [[#Somma complemento a due|somma]] 
>7. Effettuiamo la [[#Conversione (metodo circuitale)|conversione del risultato da complemento a due a decimale]]

>[!warning] Esempio
>![[IMG_C6C5249596C3-1.jpeg|800]]

---
## Casi Particolari con Somma/Sottrazione

>[!note] Somma tra numeri di cui almeno uno dei due non è negativo
>
>Quando avviene un *over-flow* in questo caso, ***non deve*** essere preso in considerazione
>	![[IMG_BB6858C56377-1.jpeg|800]]

>[!note] Over-flow somme tra due numeri negativi
>Quando si effettua una somma tra numeri negativi è *certo* che avvenga un over-flow, possono avvenire due situazioni distinte:
>
>**1. Escludendo l'overflow il bit di segno del risultato è  sbagliato (0):**
>- Soluzione: Utilizzare bit di over-flow come bit di segno			
>![[IMG_017709F20B52-1.jpeg|700]]
>
>**2. Escludendo l'overflow il bit di segno del risultato è  giusto (1)**
>- in questo caso, indipendentemente dal fatto che utilizzeremo o no il bit di overflow come bit di segno il risultato sarà giusto!	
>	![[IMG_CA1AE6C90F6D-1.jpeg|700]]

>[!note] Mancanza di bit per la rappresentazione
>Sommando c'è il rischio di non avere abbastanza bit per rappresentare il risultato
>
>- Soluzione [[#Estensione rappresentazione utilizzando complemento a due|estendere]] gli operandi e ripetere l'operazione
>	 ![[IMG_BD2B4F6ECD4F-1.jpeg|800]]

---
## Estensione rappresentazione utilizzando complemento a due 

>[!note] Estensione di numero positivo
 >Se numero inizia con 0 aggiungo tanti zeri quanto voglio estendere
 
>[!note] Estensione di numero negativo
>Se numero inizia con 1 aggiungo tanti uni quanto voglio estendere
 
>[!warning] Esempi:
>![[IMG_CF8E0AC38FD9-1.jpeg|700]]

---
## Over-flow  e Under-flow con complemento a due

Con **Over-flow** e **Under-flow** si indica il superare il numero di bit necessari per rappresentare un determinato numero rispetto al numero di bit di cui si a disposizione (limitazione che può essere imposta dall'architettura o dal software), avviene quando si operazioni sui numeri

#### [[Over-flow]]
In particolare quando questo avviene in un sistema che utilizza il complemento a due è possibile accorgersene da fatto che il bit del segno assume valori impossibili. (esempio la somma di due numeri negativi da un risultato positivo)

>**oss:** basta controllare bit di segno per verificare l'avvenimento di un over-flow

Per calcolare il numero risultante dobbiamo calcolare di quanto stiamo "sforando" es. se vogliamo rappresentare il numero 9 ma la nostra architettura (4bit) permette di rappresentare massimo il 7 stiamo "sforando" di *2*, quando si sfora in realtà si sta saltando dal lato opposto del range e si avanza di quanto si a sforato

>[!warning] Esempio
>![[IMG_overflow.jpeg|800]]

#### [[Under-flow]]
In particolare si parla di **Under-flow** quando proviamo a rappresentare un numero Negativo più piccolo rispetto al numero negativo minimo rappresentabile dal numero di bit a disposizione.

Per risolvere dobbiamo fare aumentare il numero di bit a nostra disposizione per la rappresentazione utilizzando in metodo dell' estensione 

>[!tip] Estensione
> Per estendere un numero basta aggiungere un nuovo bit più significativo (tutto a sinistra), in particolare in CA2 se dobbiamo estendere un numero:
> - *Positivo:* aggiungiamo uno 0 
> - *Negativo:* aggiungiamo un 1

>[!warning] Esempio
>![[IMG_underflow.jpeg|800]]
