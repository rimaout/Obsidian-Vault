---
Created: 2024-05-02
Type: Uni Note
Class:
  - "[[Calcolo Integrale (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Integrali]]"
Completed: true
---
---

>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Esempi]]
>3. [[#Integrare per parti due o più volte]]
>4. [[#Integrali Ciclici]]
>5. [[#Fattore differenziale 1]]

>[!abstract] Related
>- [[Integrali]]
>- [[Calcolo Integrale (class)]]

---
## Introduzione

Metodo utilizzato per semplificare integrali nella forma $\int f(x)\, g'(x)\, dx$, dove il prodotto tra funzioni $f(x)\cdot g^{\prime}(x)$ è integrabile.

>[!info] Formula Integrali Definiti
>
>$$
>\int^{b}_{a} f(x)\, g'(x)\, dx\ = \ f( b )\, g(b) -  f( a )\, g(a)-\int^{b}_{a} f'(x)\, g(x)\, dx 
>$$

>[!info] Formula Integrali Definiti
>
>$$
>\int f(x)\, g'(x)\, dx\ = \ f( x )\, g(x)- \int f'(x)\, g(x)\, dx 
>$$

>[!warning] Quando utilizzarlo
> L'obbiettivo di questo metodo è quello di trasformare l’integrale originale in un’altra forma più facile da calcolare, ma non è assicurato la nuova forma sia più semplice dell'originale

---
## Come usare la formula

Individuare, tra le due funzioni, la derivata $g'(x)$ e la primitiva $f(x)$:
- La **derivata** da individuare, $g(x)$, deve avere una **primitiva** immediata da calcolare.
- La **primitiva** $f(x)$ deve avere una **derivata** $f'(x)$ che semplifichi il nuovo integrale $\int f'(x)\, g(x) \ dx$.

---
## Esempi

>[!info] Esempio 1
>![[signal-2024-05-02-171324_002.png|500]]

>[!info] Esemepio 2
>![[signal-2024-05-02-171405_002.png|500]]

>[!info] Esempio 3
>![[signal-2024-05-02-171419_002.png|650]]
>In questo caso serve effettuare l'integrazione per parti più volte vedi [[#Integrare per parti due o più volte]] per altri esempi

>[!info] Esempio 4
>![[signal-2024-05-02-173430_002.png|500]]

---
## Integrare per parti due o più volte

Quando si hanno integrali di funzioni con derivate cicliche, come ad esempio $\textcolor{orange}{\int x^{\alpha}\cdot \sin (x)\,dx}$, $\textcolor{orange}{\int x^{\alpha}\cdot\cos(x)\,dx}$ e $\textcolor{orange}{\int x^{\alpha}\cdot e^{x}\,dx}$ può capitare di dover riapplicare l'integrazione per parti sul risultato dell'iterazione precedente.

>[!info] Esempio 
>![[Pasted image 20240506172201.png|700]]

---
## Integrali Ciclici

Nei casi in l'integrale sia composto dal prodotto di due funzioni con derivate cicliche, non è possibile risolvere l'integrale per part in maniera "classica", ma basta notare che dopo due integrazioni per parti si riottiene l'integrale originare.

Possiamo sfruttare questa caratteristica per risolvere questa uguaglianza trattandola come una normale equazione.

>[!note] Esempio
![[Pasted image 20240526123457.png|650]]

---
## Fattore differenziale 1

Quando si prova ad integrare alcune [[Funzioni Elementari]] risulta apparentemente impossibile risolverle con le "classiche" [[Integrali#^4581ca|tecniche di integrazione]].

Ad esempio con $\int \ln(x)\,dx$ e $\int \arctan(x)\, dx$ non risulta possibile utilizzare nessuna tecnica di integrazione, in particolare sembra impossibili utilizzare l'**integrazione per parti** perché non abbiamo la seconda funzione per il prodotto.

In realtà ci basta considerare $g'(x)=1$ e integrare per parti prendendolo come derivata.

>[!note] Esempio
>![[Pasted image 20240526164419.png|800]]

---


