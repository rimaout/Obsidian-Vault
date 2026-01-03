---
created: 2024-02-06
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[Registri]]"
completed: true
updated: 2024-07-09T11:23
---
>[!abstract] Indice
>1. [[#Definizione]]
>2. [[#Load]]
>3. [[#Funzionamento caricamento]]

>[!abstract] Related
>- [[Flip Flop]]
>- [[Circuiti sequenziali]]
>- [[Progettazione Sistemi Digitali (class)]]

---
## Definizione

>[!warning] Caratteristiche
>- Una sola linea di input, il **serial input**. 
>- Serie di **FF connessi in cascata**, in cui l'uscita di ogni flip flop è connessa all'entrata del successivo.
>- Segnale di **load** per assicurare che lo scorrimento dell'input si fermi, *interrompendo il caricamento*, e inizi la fase di *memorizzazione*.

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
>![[Pasted image 20240207120118.png|500]]
>$$
>\text{Load} = \begin{cases}
>0 & \to S=0,\ R=0 \to \text{Memorizzazione} \\
>1 & \to S=si, R=\overline{si} \to \text{Funzionamento FF D}
>\end{cases} 
>$$
>
>**FF D:** 
>
>![[Pasted image 20240207112339.png|500]]
>$$ 
>\text{Load} = \begin{cases}
>0 & \to D=y \to \text{Memorizzazione} \\
>1 & \to S=si \to \text{Funzionamento FF D}
>\end{cases}
>$$
^d80083

>[!warning] Load sul clock
>![[Pasted image 20240206195051.png|500]]
^3ab1ca

 >[!warning] oss
 >Tutti questi esempi sono con scorrimento a destra

---
## Funzionamento caricamento

>[!warning] Funzionamento 
> 1. Registro composto da n flip flop in cascata con caricamento seriale
> 2. Load deve essere impostato ad 1 
> 3. Ad ogni fronte d'onda del clock il contenuto dei flip flop verra shiftato a destra.
> 4.  Dopo n cicli di clock il caricamento sarà finito e il load può tornare a 0

>[!warning] Esempio
>Caricare in serie 1001 con scorrimento a destra
>
>![[Pasted image 20240207145148.png|700]]
