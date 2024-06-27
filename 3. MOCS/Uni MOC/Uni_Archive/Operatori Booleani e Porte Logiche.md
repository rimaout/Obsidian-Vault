---
created: 2023-10-06
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[Algebra Booleana]]"
completed: true
updated: 2024-06-27T20:13
---
>[!abstract] Index
>1. [[#NOT]]
>2. [[#OR]]
>3. [[#AND]]
>4. [[#NOR]]
>5. [[#NAND]]
>6. [[#XOR]]
>7. [[#Porte logiche con più variabili in ingresso]]

>[!abstract] Related
>- [[Algebra Booleana]]
>- [[Progettazione Sistemi Digitali (class)]]

---
## NOT

- **Operazione:** Negazione Logica
- **Significato:** L’uscita assume il valore logico opposto a quello applicato in ingresso

>[!note] Info
>![[IMG_6ADBFBCE93F2-1.jpeg|500]]

---
## OR

- **Operazione:** Somma Logica
- **Significato:** L’uscita assume lo stato logico 1 se almeno una variabile di ingresso è allo stato logico 1

>[!note] Info
>![[IMG_E9DF6517C2BE-1.jpeg|500]]

---
## AND

- **Operazione:** Moltiplicazione logica
- **Significato:** L’uscita assume lo stato logico 1 solo se tutte variabile di ingresso sono allo stato logico 1

>[!note] Info
>![[IMG_2A3698EA94BA-1.jpeg|500]]

----
## NOR

- **Operazione:** Negazione della somma logica
- **Significato:** L’uscita assume lo stato logico 0 se almeno una variabile di ingresso è allo stato logico 1

>[!note] Info
>![[IMG_735524E20D74-1.jpeg|500]]

---
## NAND

- **Operazione:** Negazione del prodotto logico
- **Significato:** L’uscita assume lo stato logico 0 se tutte le variabili di ingresso sono allo stato logico 1

>[!note] Info
>![[IMG_39F905AD281A-1.jpeg|500]]

---
## XOR

- **Operazione:** OR Esclusivo (somma logica esclusiva)
- **Significato:** L’uscita vale 1 se gli ingressi assumono valore diverso, vale 0 se gli ingressi sono tra loro uguali
- **Formula:**  $x \oplus y=\overline{x}y+x\overline{y}$

>[!note] Info
>![[img_dc1f1f583f6d-1.jpeg|500]]

>[!warning] Proprietà
>**Negazione XOR**
>- *Formula:* $\overline{x\oplus y}=x\ y+\overline{x}\ \overline{y}$
>- *Dimostrazione:* 
>
>$$
>\overline{x\oplus y}= \overline{\overline{x}y+ x\overline{y}}=(x+\overline{y}) \cdot(\overline{x}+y)=x\overline{x}+xy+\overline{x}\ \overline{y}+y\overline{y}=xy+\overline{x}\ \overline{y}
>$$

---
## Porte logiche con più variabili in ingresso

>[!note] Esempio
>![[IMG_7609DBA96BB5-1.jpeg|600]]
