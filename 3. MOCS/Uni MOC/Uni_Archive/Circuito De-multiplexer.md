---
created: 2024-02-02
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[Circuiti combinatori]]"
completed: true
updated: 2024-05-27T13:29
---
---
## Index
1. [[#Definizione]]
2. [[#Calcolo numero variabili]]
3. [[#Circuito interno]]
4. [[#DEMUX Tree]]

---
## Definizione

É un circuito combinatorio che selezione segnali binari provenienti da una o più linee in input e li dirige in una sola uscita

>[!warning] Rappresentazione circuitale
>![[Pasted image 20240202104407.png|350]]

**Utilizzi:**
1. Ridurre numero di linee
2. Riduzione complessità e costo di un circuito
3. Implementazione di altri circuiti (es: [[Half-Adder]], [[Full-Adder]])

---
## Calcolo numero variabili

*Input* = 1
*Output* = n
*Selection* = $\log_{2}n$

---
## Circuito interno
- Insieme di porte [[Operatori Booleani e Porte Logiche#AND|AND]]

>[!warning] MUX 1-2:
![[Pasted image 20240123113632.png|600]]

>[!warning] MUX 1-4:
>![[Pasted image 20240202120322.png|600]]

---
## DEMUX Tree

>[!tip] 
> È possibile unire due circuiti de-multiplexer tra loro per crearne uno più grande

![[demux.png|800]]

---