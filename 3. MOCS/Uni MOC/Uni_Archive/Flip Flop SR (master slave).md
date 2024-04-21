---
Created: 2024-02-05
Type: Uni Note
Class:
  - "[[Progettazione Sistemi Digitali (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Latch]]"
  - "[[Flip Flop]]"
Completed: true
---
---
## Index
1. [[#Definizione]]
2. [[#Circuito + Funzionamento]]

---
## Definizione
Il **FF SR Master Slave** è un circuito [[Circuiti sequenziali|sequenziale]], [[Circuiti Sincroni ed Asincroni#Circuiti Sincroni|sincrono]], *edge triggered* utilizzato per memorizzare un singolo bit di informazione.

>[!warning] Simbolo
> ![[Pasted image 20240205171808.png|200]]

## Circuito + Funzionamento
- Un Flip Flop master slave è composto da due latch collegati in serie, il **master** (a sinistra) e lo **slave** (a destra) entrambi collegati al segnale di clock, il quale è negato per l'ingresso allo slave.
- L'output del master è collegato all'input dello slave. 

>[!warning] Circuito
>![[Pasted image 20240205172751.png|450]]

>[!warning] Funzionamento
>Il master legge i valori di input quando il valore del clock è a 1, mentre lo slave è abilitato solo quando il clock è a 0. Perciò un segnale di input non può passare immediatamente come accadeva per il latch, ma l'output sarà verificato solo nella seconda fase del ciclo del clock (= 0).
>
>**oss:** Gli output dello *slave* sono sempre uguali a gli output del *master*

>[!warning] Tabelle di verità
>![[Pasted image 20240205175237.png|350]]
>
>**oss:** y = y(y) e Y = y(t+1)

>[!warning] Formula
$Y = \overline{R} \cdot (S+y)$
>- y = y(t)
>- Y = y(t+1)
>
>**oss:** Formula FF SR =  [[Latch SR#Formula|Formula Latch SR]]

---