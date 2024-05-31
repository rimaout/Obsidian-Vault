---
created: 2024-05-15
type: Uni Note
class:
  - "[[Introduzione agli Algoritmi (class)]]"
academic year: 2023/2024
related:
  - "[[Alberi (Struttura Dati)]]"
completed: true
updated: 2024-05-27T13:29
---
---

>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Visita in preordine (preorder)]]
>3. [[#Visita inordine (inorder)]]
>4. [[#Visita postordine (postorder)]]
>5. [[#Visite per Livelli]]
>6. [[#Costo temporale delle visite]]

>[!abstract] Related
>- [[Introduzione agli Algoritmi (class)]]
>- [[Alberi (Struttura Dati)]]

---
## Introduzione

L’**accesso progressivo a tutti i nodi** di un albero si chiama visita dell’albero.

>[!info] Tipi di visite
>Nel caso degli [[Alberi Binari (Struttura Dati)|alberi binari]], nei quali i figli di ogni nodo (e quindi i sottoalberi) sono al massimo due, le possibili decisioni in merito a questa scelta danno luogo a tre diverse visite:
>- [[#Visita in preordine (preorder)]]
>- [[#Visita inordine (inorder)]]
>- [[#Visita postordine (postorder)]]

>[!info] Esempio
>![[Pasted image 20240515104958.png|400]]
>
>- Preordine: $\big[\textcolor{orange}{\text{a - f - z - g - b - g}}\big]$
>- Inordine: $\big[\textcolor{orange}{\text{z - f - g - a - b - k}}\big]$
>- Postordine: $\big[\textcolor{orange}{\text{z - g - f - k - b - a}}\big]$

---
## Visita in preordine (preorder)

Nella visita in preordine il nodo è visitato prima di proseguire la visita nei suoi sottoalberi.

>[!info] Ordine
>![[Pasted image 20240515110654.png|400]]
>
>**Esempio:** $\big[\textcolor{orange}{\text{a - f - z - g - b - g}}\big]$

>[!warning] Esempio Stampa
>
>```python
>def StampaABPreorder(p):
>	if p == none: return None
>	
>	print(p.key)
>	StampaABPreorder(p.left)
>	StampaABPreorder(p.right)
>```

---
## Visita inordine (inorder)

Nella visita inordine il nodo corrente è visitato dopo la visita del sottoalbero sinistro e prima di quella del sottoalbero destro.

>[!info] Ordine
>![[Pasted image 20240515110827.png|400]]
>
>**Esempio:** $\big[\textcolor{orange}{\text{z - f - g - a - b - k}}\big]$

>[!warning] Esempio Stampa
>
>```python
>def StampaABInorder(p):
>	if p == none: return None
>	
>	StampaABPreorder(p.left)
>	print(p.key)
>	StampaABPreorder(p.right)
>```

---
## Visita postordine (postorder)

Nella visita in postordine il nodo corrente è visitato dopo entrambe le visite dei sottoalberi.

>[!info] Ordine
>![[Pasted image 20240515110919.png|400]]
>
>**Esempio:** $\big[\textcolor{orange}{\text{z - g - f - k - b - a}}\big]$


>[!warning] Esempio Stampa
>
>```python
>def StampaABPostorder(p):
>	if p == none: return None
>	
>	StampaABPreorder(p.left)
>	StampaABPreorder(p.right)
>	print(p.key)
>```

---
## Costo temporale delle visite

Indipendentemente del tipo di visita che utilizziamo, visitare interamente un albero binario un albero binario richiede $\Theta(n)$.

Nel caso di un [[Memorizzazione tramite puntatori (Alberi Binari)|albero binario rappresentato attraverso un record a puntatori]], l' equazione di ricorrenza della visita dell'albero è:

$$
\begin{align*}
& T(n) = T(k)+T(n-k-1) + \Theta(1)\\
& T(1) = \Theta(1)
\end{align*}
$$

>[!note]- Risoluzione per Metodo Sostituzione
>
>>[!danger] Leggi Teoria [[Metodo Sostituzione (algoritmi ricorsivi)|Metodo Sostituzione]]
>>- Esempio pratico: [link](https://github.com/CS-Swap/Algoritmi-1/issues/64)
>
>>[!warning] Dimostrare
>>$T(n) \in \Theta(n)$ ovvero:
>>- $T(n)\leq c \cdot n$ ($O$)
>>- $T(n) \geq c \cdot n$ ($\Omega$)
>
>>[!note] Eq. Ricorrenza Senza Asintotica
>>$$
>>\begin{align*}
>>& T(n) = T(k)+T(n-k-1) + b\\
>>& T(1) = a
>>\end{align*}
>>$$
>
>#### Dimostrazione $O$
>
>**Dimostrare:** $T(n)\leq c \cdot n$
>
>>[!note] Caso Base $(n=1)$
>>$$
>>\begin{align*}
>>&T(n) \leq c \cdot n\\
>>&T(1) \leq c \cdot 1\\
>>&\textcolor{orange}{a\leq c}
>>\end{align*}
>>$$
>
>>[!note] Ipotesi Induttiva
>>- $T(k)\leq c\cdot k$
>>- $T(n-1-k) \leq c \cdot(n-1-k)$
>
>>[!note] Passo Induttivo
>>$$
>>\begin{align*}
>>&T(n)\leq c \cdot n\\
>>&T(k) + t(n-1-k) + b\leq c\cdot n\\
>>&\cancel{ ck } + \cancel{ cn } - c - \cancel{ ck } + b \leq \cancel{ cn }\\
>>&\textcolor{orange}{b\leq c}
>>&\end{align*}
>>$$
>
>**Quindi:** $T(n)\in O(n)$
>
>#### Dimostrazione $\Omega$
>
>**Dimostrare:** $T(n)\geq c \cdot n$
>
>>[!note] Caso Base $(n=1)$
>>$$
>>\begin{align*}
>>&T(n) \geq c \cdot n\\
>>&T(1) \geq c \cdot 1\\
>>&\textcolor{orange}{a\geq c}
>>\end{align*}
>>$$
>
>>[!note] Ipotesi Induttiva
>>- $T(k)\geq c\cdot k$
>>- $T(n-1-k) \geq c \cdot(n-1-k)$
>
>>[!note] Passo Induttivo
>>$$
>>\begin{align*}
>>&T(n)\geq c \cdot n\\
>>&T(k) + t(n-1-k) + b\geq c\cdot n\\
>>&\cancel{ ck } + \cancel{ cn } - c - \cancel{ ck } + b \geq \cancel{ cn }\\
>>&\textcolor{orange}{b\geq c}
>>&\end{align*}
>>$$
>
>**Quindi:** $T(n)\in \Omega(n)$
>
>#### Dimostrazione $\Theta$
>
>Visto che $\exists c_{1}\ t.c.\ T(n)\leq c_{1}\cdot n$ e $\exists c_{2}\ t.c.\ T(n)\geq c_{2}\cdot n$ 
>- Allora $T(n)\in \Theta(n)$

---
## Visite per Livelli

---
## Applicazione delle visite
Le visite sono estremamente utili per ispezionare l’albero e dedurne delle proprietà.

A seconda delle proprietà che si vuole esaminare può essere più utile una delle tre visite considerate

**Esempi di visite:** [[Esercizi visite alberi binari]] 🟢

---

