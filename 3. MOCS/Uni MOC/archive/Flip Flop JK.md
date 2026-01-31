---
created: 2024-02-05
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[Circuiti sequenziali]]"
  - "[[Latch]]"
  - "[[Flip Flop SR (master slave)]]"
completed: true
updated: 2026-01-31T13:32
---
>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Circuito + Funzionamento]]

>[!abstract] Related
>- [[Flip Flop]]
>- [[Circuiti sequenziali]]
>- [[Progettazione Sistemi Digitali (class)]]

---
## Introduzione

Il **FF JK** è un circuito [[Circuiti sequenziali|sequenziale]], [[Circuiti Sincroni ed Asincroni#Circuiti Sincroni|sincrono]], *edge triggered* derivato dal [[Flip Flop SR (master slave)]].

>**oss:** A differenza del flip flop SR utilizza la combinazione 11 per negare lo stato prendete.

>[!warning] Simbolo
>![[Pasted image 20240205190135.png|200]]

---
## Circuito + Funzionamento

- Un Flip Flop master slave è composto da due latch collegati in serie, il **master** (a sinistra) e lo **slave** (a destra) entrambi collegati al segnale di clock, il quale è negato per l'ingresso allo slave.
- L'output del master è collegato all'input dello slave. 

>[!warning] Circuito
>![[Pasted image 20240205225446.png|350]]

>[!warning] Funzionamento
> Funzionamento identico al [[Flip Flop SR (master slave)|FF SR]], ma quando J = 1 e K = 1 --> Y = $\overline{y}$

>[!warning] Tabelle di verità
>![[Pasted image 20240205192416.png|400]]
>
>**oss:** y = y(y) e Y = y(t+1)

>[!warning] Formula
>$Y =y\overline{K}+ \overline{y}J$ 
>
>**Ricavare formula da tavola della verità:**
>![[Pasted image 20240205195038.png|300]]
>
>**Ricavare formula da FF SR:**
>- *Formula FF SR:* $Y = \overline{R} \cdot (S+y)$ 
>- In FF JK:
>	- $S = J\overline{y}$
>	- $R = Ky$
> 
> *Formula FF JK:* $Y = \overline{Ky} \cdot (J\overline{y}+y)$  = $y\overline{K}+ \overline{y}J$ 
