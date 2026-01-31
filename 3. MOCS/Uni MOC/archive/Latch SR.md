---
created: 2023-11-06
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[Circuiti sequenziali]]"
completed: true
updated: 2026-01-31T13:32
---
>[!abstract] Index
>1. [[#Definizione]]
>2. [[#Circuito + Funzionamento]]
>3. [[#Formula]]
>4. [[#Studio degli stati]]

>[!abstract] Related
>- [[Latch]]
>- [[Circuiti sequenziali]]
>- [[Progettazione Sistemi Digitali (class)]]

---
## Definizione

- Il **Latch SR** (latch set and reset) è un circuito [[Circuiti sequenziali|sequenziale]], [[Circuiti Sincroni ed Asincroni#Circuiti Asincroni|asincrono]] base utilizzato per la memorizzazione di un bit.
- È il tipo di lath più semplice, costruito a partire da due porte [[Operatori Booleani e Porte Logiche#NOR|nor]] con collegamenti incrociati

>[!warning] Rappresentazione circuitale
>![[Pasted image 20240205111516.png|250]]

>[!warning] I/O
>**Input:**
>- *s* = Set
>- *r* = Reset
>
>**Output:**
>- *y* = Stato del latch (output)

---
## Circuito + Funzionamento

>[!warning] Circuito
>![[Pasted image 20240205112652.png|300]]

>[!warning] Funzionamento
>- Stato di **Set:** quando S = 1 --> y = 1
>- Stato di **Reset:** quando R = 1 --> y = 0
>- Stato di **Memorizzazione:** quando S = 0 e R = 0 --> y rimane invariato
>- Stato **Indefinito:** quando S = 1 e Y = 1 --> comportamento anomalo in cui entrambe le uscite sono uguali a 0

>[!warning] Tabella stati futuri
>![[Pasted image 20240205114058.png|400]]
>
>**oss:**
>- *y(t)* --> stato presente
>- *y(t+1)* --> stato futuro

---
## Formula

>[!warning] Formula
>$Y = \overline{R} \cdot (S+y)$
>- y = y(t)
>- Y = y(t+1)

>[!warning] Come ricavare formula
>![[Pasted image 20240205121007.png|450]]

>[!warning] Come vuole Prof
> - $y(t+1) = \overline{r+\overline{y(t)}} = \overline{r}+\overline{s+y(t)}=\overline{r}(s+y(t))$
> - Funziona perché  non è ammesso r = 1 e s = 1

---
## Studio degli stati

>[!warning] Set
>![[Pasted image 20240205124151.png|300]]

>[!warning] Reset
>![[Pasted image 20240205124223.png|300]]

>[!warning] Memorizzazione>
>![[Pasted image 20240205125138.png|300]]
>
>Per dimostrare che il latch mantiene lo stato precedente "tagliamo" il filo che collega l'uscita y all'entrata della porta NOR. Otteniamo così due punti (A e B). Se, partendo dal punto B, arriviamo al punto A con valore invariato, allora il latch ha
>mantenuto lo stato precedente.
