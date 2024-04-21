---
Created: 2024-02-02
Type: Uni Note
Class:
  - "[[Progettazione Sistemi Digitali (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Circuiti combinatori]]"
Completed: true
---
---
## Index
1. [[#Definizione]]
2. [[#Come programmare PLA]]
3. [[#Circuito + Esempio]]

---
## Definizione

- É un **circuito combinatorio** composto da un array programmabile di porte [[Operatori Booleani e Porte Logiche#AND|and]] seguito da un array programmabile di porte [[Operatori Booleani e Porte Logiche#OR|or]].
- PLA permette di rappresentare una qualsiasi [[Algebra Booleana#Funzioni Booleane|funzione booleana]] in forma [[Forma POS (Disgiuntiva) e SOP(Congiuntiva)|SOP]].

>[!warning] oss:
>Metodo più economico ed efficiente per rappresentare funzioni booleane rispetto a una [[ROM (read only memory)]]

---
## Come programmare PLA

1. Trovare funzione booleana in forma [[Forma POS (Disgiuntiva) e SOP(Congiuntiva)|SOP]].
2. Identificare le variabili di ingresso e gli [[Input Buffer|input buffer]].
3. Rappresentare attraverso la matrice di and i termini prodotto con le variabili o il loro complemento.
4. Rappresentare funzioni congiungendo i termini prodotto con la matrice di or.

>[!warning] oss:
>PLA permette di rappresentare più funzioni booleane alla volta

---
## Circuito + Esempio

>[!warning] Formule booleane in forma sop
>![[Pasted image 20240202170605.png|150]]

>[!warning] Oss:
>*3 input:* $A$, $B$ e $C$ (variabili in ingresso)
>*2 output:* $Y_{1}$ e $Y_{2}$ (porte or finali)
>mintermini (porte and):
>- $AC$
>- $BC$
>- $\overline{A}B\overline{C}$

>[!warning] Circuit
>![[Pasted image 20240202184254.png|500]]

---