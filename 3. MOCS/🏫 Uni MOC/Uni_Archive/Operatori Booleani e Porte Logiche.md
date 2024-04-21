---
Created: 2023-10-06
Type: Uni Note
Class:
  - "[[Progettazione Sistemi Digitali (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Algebra Booleana]]"
Completed: true
---
---
## Indice:
1. [[#NOT]]
2. [[#OR]]
3. [[#AND]]
4. [[#NOR]]
5. [[#NAND]]
6. [[#XOR]]
	- [[#Negazione XOR]]
7. [[#Porte logiche con più variabili in ingresso]]

---
## NOT
- *Negazione Logica *
- *Significato:* L’uscita assume il valore logico opposto a quello applicato in ingresso

![[IMG_6ADBFBCE93F2-1.jpeg|500]]

---
## OR
- *Somma Logica*
- *Significato:* L’uscita assume lo stato logico 1 se almeno una variabile di ingresso è allo stato logico 1

![[IMG_E9DF6517C2BE-1.jpeg|500]]


---
## AND
- *Moltiplicazione logica*
- *Significato:* L’uscita assume lo stato logico 1 solo se tutte variabile di ingresso sono allo stato logico 1

![[IMG_2A3698EA94BA-1.jpeg|500]]

----
## NOR
- *Negazione della somma logica*
- *Significato:* L’uscita assume lo stato logico 0 se almeno una variabile di ingresso è allo stato logico 1

![[IMG_735524E20D74-1.jpeg|500]]

---
## NAND
- *Negazione del prodotto logico*
- *Significato:* L’uscita assume lo stato logico 0 se tutte le variabili di ingresso sono allo stato logico 1

![[IMG_39F905AD281A-1.jpeg|500]]

---
## XOR
- *OR Esclusivo (somma logica esclusiva)*
- *Significato:* L’uscita vale 1 se gli ingressi assumono valore diverso, vale 0 se gli ingressi sono tra loro uguali
- *Formula:* 
	- $x \oplus y=\overline{x}y+x\overline{y}$
	
![[img_dc1f1f583f6d-1.jpeg|500]]

**Negazione XOR**
- *Formula:* $\overline{x\oplus y}=x\ y+\overline{x}\ \overline{y}$
- *Dimostrazione:* 

$$
\overline{x\oplus y}= \overline{\overline{x}y+ x\overline{y}}=(x+\overline{y}) \cdot(\overline{x}+y)=x\overline{x}+xy+\overline{x}\ \overline{y}+y\overline{y}=xy+\overline{x}\ \overline{y}
$$

---
## Porte logiche con più variabili in ingresso

![[IMG_7609DBA96BB5-1.jpeg|800]]

---