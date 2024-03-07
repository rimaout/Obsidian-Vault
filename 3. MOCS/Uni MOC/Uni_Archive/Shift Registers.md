---
Created: 2024-02-07
Type: Uni Note
Class:
  - "[[Progettazione Sistemi Digitali (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Registri]]"
  - "[[Caricamento Registri Seriale]]"
Completed: true
---
---
## Indice
1. [[#Definizione]]
2. [[#Right Shift Registers]]
3. [[#Left Shift Registers]]
4. [[#Bidirectional Shift Register]]

---
## Definizione
Uno **Shift register** è un insieme di [[Flip Flop]] in cascata dove l'output di un flip flop è l'input del flip flop successivo, questo permette ai dati di "shiftare" da una posizione alla successiva.

Tutti i registri a [[Caricamento Registri Seriale|caricamento seriale]] sono di base shift register ma anche un registro a [[Caricamento Registri Parallelo|caricamento parallelo]], adattando il circuito, può essere uno shift register.

Un registro a **caricamento parallelo** può è essere usato come shift register posizionando prima di ogni entrata dei [[Flip Flop]] un [[Circuito Multiplexer|MUX]] che permetta di selezionare l'entrata parallela (modalità load) o l'uscita del flip-flop precedente come entrata (modalità right shift register).

Esistono Tre tipi di Shift registe:
- [[#Right Shift Registers]]
- [[#Left Shift Registers]]
- [[#Bidirectional Shift Register]]

---
## Right Shift Registers
- Entrata del flip flop è l'uscita del flip-flop precedente.

>[!warning] SISO Right Shift Register 
>![[Pasted image 20240209122035.png|700]]

>[!def] Other:
>- [[Registro SISO#SISO Right Shift Register|SISO Right Shift Register]]
>- [[Registro SIPO#SIPO Right Shift Register|SIPO Right Shift Register]]
>- [[Registro PISO#PISO Right Shift Register|PISO Right Shift Register]]
>- [[Registro PIPO#PIPO Right Shift Register|PIPO Right Shift Register]]


---
## Left Shift Registers
- Entrata del flip flop è l'uscita del flip-flop successivo.

>[!warning] SISO Left Shift Register 
>![[Pasted image 20240209121918.png|500]]

>[!def] Other:
>- [[Registro SISO#SISO Left Shift Register|SISO Left Shift Register]]
>- [[Registro SIPO#SIPO Left Shift Register|SIPO Left Shift Register]]
>- [[Registro PISO#PISO Left Shift Register|PISO Left Shift Register]]
>- [[Registro PIPO#PIPO Left Shift Register|PIPO Left Shift Register]]

---
## Bidirectional Shift Register 
- Posizionare prima dell'entrata dei [[Flip Flop]] un [[Circuito Multiplexer|MUX]] che permetta di selezionare l'entrate l'output del flip-flop precedente (modalità right shift) o l'uscita del flip-flop successivo come entrata (modalità left shift). 

>[!warning] Circuito
>![[Pasted image 20240209114442.png|700]]
>
>$$ \text{Shift} = \begin{cases}
>1 \to \text{Right Shift} \\
>0 \to \text{Left Shift}
>\end{cases} $$

>[!def] Other:
>- [[Registro SISO#SISO Bidirectional Shift Register|SISO Bidirectional Shift Register]]
>- [[Registro SIPO#SIPO Bidirectional Shift Register|SIPO Bidirectional Shift Register]]
>- [[Registro PISO#PISO Bidirectional Shift Register|PISO Bidirectional Shift Register]]
>- [[Registro PIPO#PIPO Bidirectional Shift Register|PIPO Bidirectional Shift Register]]


---