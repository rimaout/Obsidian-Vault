---
Created: 2024-05-17
Type: Uni Note
Class:
  - "[[Calcolo Integrale (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Integrali]]"
  - "[[Integrali di Funzioni Razionali]]"
Completed: true
---
---

>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Procedura]]
>3. [[#Esempi (fattorizzazione 1° Grado)]]
>4. [[#Esempi (fattorizzazione 2° grado)]]

>[!abstract] Related
>- [[Calcolo Integrale (class)]]
>- [[Integrali di Funzioni Razionali]]
>- [[Integrali]]

---
## Introduzione
Questo è un metodo generale per la risoluzione di integrai di funzioni razionali, ovvero integrali di frazioni dove sia al numeratore che al denominatore è presente un polinomio.

>[!note] Forma
>
>$$
>\int \frac{n(x)}{d(x)} \, dx 
>$$

---
## Procedura
Questa procedura si divide in 4 fasi:

>[!note] 1\. Divisione
>
>Effettuare una [[Divisone tra polinomi|divisione polinomiale]] tra **numeratore** $n(x)$ e il **denominatore** $d(x)$.
>
>>[!danger] Importante!!
>>Questo passaggio va effettuato soltanto se $\textcolor{orange}{grd\, d(x)<grd\, n(x)}$:
>>- ovvero se Il grado grado del denominatore è maggiore del grado del numeratore.

>[!note] 2\. Fattorizzazione
>Fattorizzare il **denominatore** $d(x)$.
>- ovvero scomporre il denominatore in un prodotto di fattori di primo e/o secondo grado non ulteriormente .

^2eb300

>[!note] 3\. Decomposizione
>Decomporre la frazione in "fratti" più semplici.
>- Questo passaggio cambia in base al grado massimo dei termini della Fattorizzazione:
>	- [[#Esempi Fattorizzazione 1° Gardo]]
>	- [[#Esempi Fattorizzazione 2° Gardo]]

^58bcf8

>[!note] 4\. Integrazione
>Integrare i vari "pezzettini".

---
## Grado degli elementi della fattorizzazione

In base ai gradi degli elementi della [[#^2eb300|fattorizzazione]]  la procedura per il calcolo della [[#^58bcf8|decomposizione]] può cambiare:

![[Pasted image 20240519164227.png|800]]

---
## Esempi

>[!example] Esempio 1\. (dettagliato)
>
>>[!danger] Risolvere
>>
>>![[Pasted image 20240518103549.png|200]]
>
>>[!note] Divisione
>>
>>![[Pasted image 20240517104112.png|800]]
>
>>[!note] Fattorizzazione
>>
>>![[Pasted image 20240517131240.png|500]]
>>
>> Vedi: [[Fattorizzazione di un polinomio]]
>
>>[!note]  Decomposizione
>>
>>Riscrivere $\frac{1}{x^{2}-x-2}$ come come una somme di frazioni più semplici
>>![[Pasted image 20240519165452.png|680]]
>
>>[!note] Integrazione 
>>
>>Integriamo funzione originale ma riscritta nella sua scomposizione più semplice
>>
>>![[Pasted image 20240517155537.png|720]]

>[!example] Esempio 2\.
>![[Pasted image 20240519165249.png|700]]
  
>[!example] Esempio 3\.
>![[Pasted image 20240519165333.png|700]]

>[!example] Esempio 4\.
>![[Pasted image 20240519170611.png|850]]

>[!warning] oss
>![[Pasted image 20240519170749.png|500]]

