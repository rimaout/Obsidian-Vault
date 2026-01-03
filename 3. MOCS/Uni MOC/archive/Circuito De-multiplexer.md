---
created: 2024-02-02
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[Circuiti combinatori]]"
completed: true
updated: 2024-11-18T20:21
---
>[!abstract] Index
>1. [[#Definizione]]
>3. [[#Circuito]]
>4. [[#MUX Tree]]

>[!abstract] Related
>- [[Circuiti combinatori]]
>- [[Circuiti combinatori]]
>- [[Progettazione Sistemi Digitali (class)]]

---
## Introduzione

É un circuito combinatorio che selezione segnali binari provenienti da una o più linee in input e li dirige in una sola uscita

>[!note] Rappresentazione circuitale
>![[Pasted image 20240202104407.png|350]]

>[!note] Input / Output
>*Input* = 1
>*Output* = n
>*Selection* = $\log_{2}n$

>[!warning] Utilizzi
>1. Ridurre numero di linee
>2. Riduzione complessità e costo di un circuito
>3. Implementazione di altri circuiti (es: [[Half-Adder]], [[Full-Adder]])

---
## Circuito

>**OSS:** Insieme di porte [[Operatori Booleani e Porte Logiche#AND|AND]]

>[!warning] DEMUX 1-2:
>![[Pasted image 20240612165626.png|600]]

>[!warning] DEMUX 1-4:
>![[Pasted image 20240202120322.png|600]]

---
## DEMUX Tree

>[!tip] 
> È possibile unire due circuiti de-multiplexer tra loro per crearne uno più grande.

![[demux.png|800]]

---