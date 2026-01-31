---
created: 2024-02-06
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[Registri]]"
completed: true
updated: 2026-01-31T13:32
---
>[!abstract] Indice
>1. [[#Definizione]]
>2. [[#Load]]

>[!abstract] Related
>- [[Flip Flop]]
>- [[Circuiti sequenziali]]
>- [[Progettazione Sistemi Digitali (class)]]

---
## Definizione

>[!warning] Caratteristiche
>- n linee di caricamento (una per ogni [[Flip Flop]])
>- Caricamento quando permesso dalla sensibilità del clock.

>[!warning] Esempio
>![[Pasted image 20240206171903.png|500]]
>
>>**oss:** 
>>- Sono lo stesso circuito
>>- Per avere un mantenimento dell'informazione gli input non devono variare **(svantaggio)**

---
## Load

**Load** è un ulteriore segnale di controllo utilizzato per permettere il mantenimento dell'informazione indipendentemente degli ingressi.

$$
Load = \begin{cases} 
1 \to \text{Caricamento} \\
0 \to  \text{Memorizzazione}
\end{cases}
$$
**Esistono due tipi di load:**
- [[#^d80083|Load sugli Input]]
- [[#^3ab1ca|Load sul Clock]]

>[!warning] Load sugli Input
>**FF SR:**
>
>![[Pasted image 20240207115154.png|500]]
>
>$$
>\text{Load} = \begin{cases}
>0 &\to S=0, R=0 \to \text{Memorizzazione} \\
>1 &\to S=x, R=\overline{x} \to \text{Funzionamento FF D}
>\end{cases}
>$$
>
>**FF D:** 
>
>![[Pasted image 20240207121203.png|500]]
>
>$$
>\text{Load} = \begin{cases}
>0 &\to D=y \to \text{Memorizzazione} \\
>1 &\to S=x\to \text{Funzionamento FF D}
>\end{cases}
>$$
^d80083

>[!warning] Load sul clock
>![[Pasted image 20240206175705.png|500]]
^3ab1ca