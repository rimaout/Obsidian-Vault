---
Created: 2023-11-06
Type: Uni Note
Class:
  - "[[Progettazione Sistemi Digitali (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Circuiti sequenziali]]"
  - "[[Latch SR]]"
Completed: true
---
---
## Index
1. [[#Definizione]]
2. [[#Circuito + Funzionamento]]
3. [[#Formula]]
4. [[#Studio degli stati]]

---
## Definizione
Il **Gated Latch** è un circuito [[Circuiti sequenziali|sequenziale]] ed [[Circuiti Sincroni ed Asincroni#Circuiti Sincroni|sincrono]] utilizzato per la memorizzazione di un bit

Ho un funzionamento identico al [[Latch SR]] ma è presente un **input supplementare**, ovvero un *segnale di controllo* che permette il *cambio* dei valori in *ingresso* solo per *tempi* discreti *predefiniti*.

Spesso viene utilizzato un segnale di clock come segnale di abilitazione, essendo un segnale periodico permette la sincronizzazione di più componenti sincrone

>[!warning] Simbolo
>![[Pasted image 20240205155716.png|200]]

>[!warning] Rappresentazione circuitale AND
![[Pasted image 20240205152407.png|300]]

>[!warning] I/O
>**Input:**
>- *s* = Set
>- *r* = Reset
>
>**Output:**
>- *y* = Stato del latch (output)

---
## Circuito + Funzionamento + Diagramma temporale

>[!warning] Circuito
>![[Pasted image 20240205154806.png|400]]

>[!warning] Funzionamento
>Se C = 0 --> **Memorizzazione** indipendente dai valori di S e R
>Se C = 1: 
>- Stato di **Set:** quando S = 1 --> y = 1
>- Stato di **Reset:** quando R = 1 --> y = 0
>- Stato di **Memorizzazione:** quando S = 0 e R = 0 --> y rimane invariato
>- Stato **Indefinito:** quando S = 1 e Y = 1 --> comportamento anomalo in cui entrambe le uscite sono uguali a 0
>
>**oss:** se c = 1 si comporta com [[Latch SR]] normale

>[!warning] Tabella stati futuri
>![[Pasted image 20240205155258.png|250]]
>
>**oss:**
>- *y(t)* --> stato presente
>- *y(t+1)* --> stato futuro

>[!warning] Diagramma temporale
>![[Pasted image 20240205161244.png|350]]
>
>**oss:** latch è abilitato per tutto il periodo in cui il clock vale 1

---
