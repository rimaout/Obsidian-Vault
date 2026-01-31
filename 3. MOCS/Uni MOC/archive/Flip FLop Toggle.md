---
created: 2024-02-05
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[Flip Flop]]"
  - "[[Circuiti sequenziali]]"
  - "[[Flip Flop JK]]"
completed: true
updated: 2026-01-31T13:32
---
>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Funzionamento]]

>[!abstract] Related
>- [[Flip Flop]]
>- [[Circuiti sequenziali]]
>- [[Progettazione Sistemi Digitali (class)]]

---
## Introduzione

Il **FF Toggle** è un circuito [[Circuiti sequenziali|sequenziale]], [[Circuiti Sincroni ed Asincroni#Circuiti Sincroni|sincrono]], *edge triggered* derivato dal [[Flip Flop JK]], ponendo J = K.

>[!warning] Circuito
>![[Pasted image 20240205200806.png|250]]

---
## Funzionamento

>[!warning] Funzionamento
>Il **Flip Flop Toggle** ha soltanto due  *memorizzazione* e *toggle*, dome memorizzazione mantiene 

>[!warning] Tabelle di verità
>![[Pasted image 20240205201326.png|300]]
>
>>**oss:** y = y(y) e Y = y(t+1)

>[!warning] Formula
>$Y = \overline{R} \cdot (S+y)$
>- y = y(t)
>- Y = y(t+1)
>
>>**oss:** Formula FF SR =  [[Latch SR#Formula|Formula Latch SR]]
