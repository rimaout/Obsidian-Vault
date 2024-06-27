---
created: 2024-02-02
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[Circuiti combinatori]]"
completed: true
updated: 2024-06-28T00:45
---
>[!abstract] Index
>1. [[#Introduzione]]
>3. [[#Programmare PLA]]
>4. [[#Circuito + Esempio]]

>[!abstract] Related
>- [[Circuiti Combinatori]]
>- [[Circuiti combinatori]]
>- [[Progettazione Sistemi Digitali (class)]]

---
## Introduzione

- É un **circuito combinatorio** composto da un array programmabile di porte [[Operatori Booleani e Porte Logiche#AND|and]] seguito da un array programmabile di porte [[Operatori Booleani e Porte Logiche#OR|or]].
- PLA permette di rappresentare una qualsiasi [[Algebra Booleana#Funzioni Booleane|funzione booleana]] in forma [[Forma POS (Congiuntiva) e SOP (Disgiuntiva)|SOP]].

>**OSS:** Metodo più economico ed efficiente per rappresentare funzioni booleane rispetto a una [[ROM (read only memory)]]

---
## Programmare PLA

1. Trovare funzione booleana in forma [[Forma POS (Congiuntiva) e SOP (Disgiuntiva)|SOP]].
2. Identificare le variabili di ingresso e gli [[Input Buffer|input buffer]].
3. Rappresentare attraverso la matrice di and i termini prodotto con le variabili o il loro complemento.
4. Rappresentare funzioni congiungendo i termini prodotto con la matrice di or.

>**OSS:** PLA permette di rappresentare più funzioni booleane alla volta

---
## Circuito + Esempio

>[!warning] Formule booleane in forma sop
>![[Pasted image 20240202170605.png|150]]

>[!warning] Oss:
>- **3 Input:** $A$, $B$ e $C$ (variabili in ingresso)
>- **2 Output:** $Y_{1}$ e $Y_{2}$ (porte or finali)
>- **Mintermini** (porte and): $AC$, $BC$, $\overline{A}B\overline{C}$

>[!warning] Circuito
>![[Pasted image 20240202184254.png|500]]
