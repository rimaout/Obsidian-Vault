---
created: 2024-02-29
type: Uni Note
class:
  - "[[Calcolo Integrale (class)]]"
academic year: 2023/2024
related:
  - "[[Successioni Reali]]"
completed: true
updated: 2024-05-27T13:29
---
---

>[!info] Index
>1. [[#Definizione di Serie]]
>2. [[#Successione delle somme parziali]]
>3. [[#Limite somme parziali]]
>4. [[#Limite della Successione]]
>5. [[#Esempi]]

---
## Definizione di Serie

>[!info] Serie
>Data una successione reale $\{a_{n}\}$, si chiama **serie** dei termini $a_{n}$ la somma degli infiniti termini della successione

La serie viene indicata con $\sum^{\infty}_{n=0}a_{n}$ che si legge serie o somma per $n$ che va da $0$ a $\infty$ di $a_{n}$ 

---
## Successione delle somme parziali 

Una **successione delle somme parziali della serie** $\{ S_{n} \}$ è la somma tra gli elementi di una serie finita.

>[!def] Definizione
>Data $\{ a_{k} \}_{k\in \mathbb{N}}$ poniamo $S_{n} = \sum_{k=0}^{n}a_{k}$
>-  dove $S_{n}$ è la successione delle somme parziali.

>[!example] Esempio
>- $S_{0} = a_{0}$
>- $S_{1} = a_{1} + a_{2}$
>- $S_{3} = a_{1} + a_{2} + a_{3}$
>
> $S_{n} = a_{0} + a_{1} + a_{2} + a_{3} + \dots + a_{n} = \sum_{k=0}^{n} a_{k}$

>[!warning] oss
>Se esiste limite per $n\to \infty$ di  $S_{n}$ allora quel limite definisce la [[Serie Numeriche#Definizione di Serie|serie numerica]].
>$$\sum^{\infty}_{n=0}a_{n} = \lim_{ n \to \infty } S_{n} = \lim_{ n \to \infty } \sum^{n}_{k=0}a_{k} $$

---
## Limite somme parziali

Facendo il limite a $+\infty$ si una somma parziale $\{ S_{n} \}$ possiamo ottenere 4 possibili risultati diversi:

$$

S_{ n } = \sum^{+\infty }_{n=1}a_{k}
$$

>[!note] Serie convergente ad un numero finito
>$$ \lim_{ n \to +\infty } S_{n} = \ell \in\mathbb{R}$$

>[!note] Serie divergente a +∞
>$$ \lim_{ n \to +\infty } S_{n} = +\infty $$

>[!note] Serie divergente a -∞
>$$ \lim_{ n \to +\infty } S_{n} = -\infty $$

>[!note] Serie indeterminata
>$$ \lim_{ n \to +\infty } S_{n} \text{ non esiste}$$
>- ovvero se successione $\{ S_{n} \}$ è oscillante $\implies$ $\lim_{ n \to \infty }S_{n}$ è indeterminato

>[!warning] oss
> Una serie a positivi non pò essere indeterminata

---
## Limite della Successione

>[!danger] $a_{ n }$ non Infinitesima
>- Se $\lim_{ n \to \infty } a_{ n } \not =0$
>- Allora $\sum_{n=1}^{+\infty}a_{ n }=+\infty$ (diverge)

>[!danger] $a_{ n }$ Infinitesima
>Se $a_{ n }$ è infinitesima 
>- Se $\lim_{ n \to \infty } a_{ n } = 0$
>- Allora non sappiamo come si comporta $\sum^{+\infty}_{n=1}a_{ n }$

---
## Esempi

>[!example] Serie convergente
>$a_{n}=0\ \forall n\in\mathbb{N}$ --> $S_{n} = 0\ \forall n \in \mathbb{N }$      
>- Quindi $\sum_{n=0}^{\infty} a_{n}\ \text{ converge a }0$ 

>[!example] Serie divergente a +∞
>$a_{n}=1\ \forall n\in\mathbb{N}$ --> $S_{n} = n+1\ \forall n \in \mathbb{N }$      
>- Quindi $\sum_{n=0}^{\infty} a_{n}\ \text{ diverge a }+\infty$ 

>[!example] Serie divergente a -∞
>$a_{n}=-1\ \forall n\in\mathbb{N}$ --> $S_{n} = -(n+1)\ \forall n \in \mathbb{N}$      
>- Quindi $\sum_{n=0}^{\infty} a_{n}\ \text{ diverge a } -\infty$ 

>[!example] Serie Indeterminata
>![[Pasted image 20240229174859.png|750]]
---

