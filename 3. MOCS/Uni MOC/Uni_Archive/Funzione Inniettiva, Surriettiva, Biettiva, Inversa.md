---
created: 2023-05-12
type: Uni Note
class:
  - "[[Metodi matematici per l'informatica (class)]]"
related:
  - "[[Funzioni]]"
completed: true
updated: 2024-06-28T14:39
---

>[!abstract] Index
>1. [[#Funzione Inniettiva]]
>2. [[#Funzione Surriettiva]]
>3. [[#Funzione Biettiva o Biunivoca]]
>4. [[#Funzione Inversa]]

>[!abstract] Related
>- [[Funzioni]]
>- [[Matematica 0 (class)]] 

---
## Funzione Inniettiva
Funzione che associa a elementi distinti del [[Funzioni#Dominio e Co-dominio|Dominio]] elementi diversi del [[Funzioni#Dominio e Co-dominio|Co-dominio]]

>**Ovvero:** Due elementi diversi del [[Funzioni#Dominio e Co-dominio|Dominio]] non possono avere la stessa [[Funzioni#Immagine|Immagine]] 

>[!note] Definizione Matematica
>$$
>f~A\to B:=\{ x,y\in A:x\not =y~~e~~f(x)\not =f(y)\}\\
>$$

>[!warning] Esempio
>![[IMG_FBCE17BE7908-1.jpeg|600]]
>![[IMG_D5D514234762-1 2.jpeg|600]]

---

## Funzione Surriettiva

Una funzione *f* è surriettiva se per ogni elemento *b* del  [[Funzioni#Dominio e Co-dominio|Co-dominio]] esiste almeno un elemento *a* del [[Funzioni#Dominio e Co-dominio|Dominio]] tale per cui *b* è l'[[Funzioni#Immagine|Immagine]] di a mediante *f*,

>**Ovvero:** Funzione che associa ad ogni elemento del [[Funzioni#Dominio e Co-dominio|Co-dominio]] almeno un elemento del [[Funzioni#Dominio e Co-dominio|Dominio]] 

>[!note] Definizione Matematica
>$$ fA\to B:=\{\forall b\in B \implies \exists a\in A:~f(b)=a \} $$

>[!warning] Esempio
>![[IMG_A64DF460974D-1.jpeg|600]]
>![[IMG_3B5904571666-1 2.jpeg|500]]

---

## Funzione Biettiva o Biunivoca

Funzione che è sia **Inniettiva** che **Surriettiva**.

>[!warning] Osservazione
>Una Funzioni Biettiva si può invertire --> [[Funzioni Invertibili]]
>$$\forall B \in b\ \ \ \ \exists!x\in A:f(x=y) $$
>
>>**ovvero*:* per ogni elemento del co-dominio è associato un solo elemento del dominio 

---

## Funzione Inversa

Se una funzione è biunivoca allora è [[Funzioni Invertibili|invertibile]].

>[!note] Notazione
>$$ 
>\begin{align*}
>& f^{-1}:A\to B \\
>&\ \ \ \ \ \ \ \ \ \ y\to x: f(x)=y \\
>& \\
>& \textcolor{orange}{Oppure:}~~f:B\to A\\
>\end{align*}
>$$

>[!warning] Esempio
>![[IMG_EB8F3C861041-1.jpeg|300]]

