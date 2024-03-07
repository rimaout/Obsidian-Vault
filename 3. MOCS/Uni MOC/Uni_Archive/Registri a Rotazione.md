---
Created: 2024-02-09
Type: Uni Note
Class:
  - "[[Progettazione Sistemi Digitali (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Registri]]"
  - "[[Shift Registers]]"
Completed: true
---
---
## Index
1. [[#Definizione]]
2. [[#Right Rotation]]
3. [[#Left Rotation]]
4. [[#Bidirectional Rotation]]

---
## Definizione
I registri a rotazione (circolari) sono degli [[Shift Registers]] dove l'**uscita** dell'ultimo [[Flip Flop]] è collegato all'**entrata** del primo e **non è presente il serial input**.

---
## Right Rotation

>[!warning] Circuito
>![[Pasted image 20240209153657.png|600]]

---
## Left Rotation

>[!warning] Circuito
>![[Pasted image 20240209154234.png|500]]

---
## Bidirectional Rotation

>[!warning] Circuito
>![[Pasted image 20240209161303.png|700]]
>
>$$\text{RR/RL} = \begin{cases}
> 1 \to \text{Rotate Right} \\
> 0 \to \text{Rotate Left}
>\end{cases}$$


---