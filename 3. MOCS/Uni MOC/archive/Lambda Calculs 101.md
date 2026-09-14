---
type: Uni Note
class:
  - "[[TPFI]]"
academic year: 2024/2025
related:
completed: false
created: 2026-06-11T11:09
updated: 2026-07-13T12:16
---
**Vedere Assolutamente:** 
- https://www.youtube.com/watch?v=ViPNHMSUcog
- https://stackoverflow.com/questions/29756732/how-would-the-lambda-calculus-add-numbers
- https://en.wikipedia.org/wiki/Church_encoding

## Perché studiamo il Lambda Calcolo? (Anima e Corpo)

Possiamo vedere le funzioni in due modi diverse:
- **Visione Matematica Classica (Anima):** Una funzione è una relazione statica tra insiemi. È la ***semantica***.
- **Lambda Calcolo (Corpo):** Qui la funzione è un **processo meccanico di calcolo**. Ci interessa la ***sintassi***, ovvero le regole scritte per trasformare un termine in un altro fino ad arrivare al risultato.

Quindi il $\lambda$-calcolo è il "motore" sotto il cofano di linguaggi come Haskell.

## Sintassi e Computazione 

La **BNF (Backus-Naur Form)** è il metalinguaggio usato per definire la grammatica rigida di un linguaggio. La grammatica del λ-calcolo puro si riduce a una sola riga:

$$
M,N \Coloneqq x \mid \lambda x.M \mid (M N)
$$

Significa che un **Termine Lambda (M o N)** può assumere solo tre forme:
- **Variabile (x):** Semplici nomi di elementi (es. `x,y,z`).
- **Astrazione (λx.M):** La definizione di una funzione anonima che prende come parametro la variabile `x` e ha come corpo il termine `M`.
    - _In Haskell:_ Corrisponde alla sintassi `\x -> M`.
- **Applicazione (M N):** La chiamata di una funzione. Significa "applica il primo termine `M` (la funzione) al secondo termine `N` (l'argomento)".

>[!note] Regole di associazione  
>- *Astrazione associa a destra*: $\lambda x_{1} \dots x_{n}.M$ equivale a $\lambda x1.(\lambda x_{2}.(\dots(\lambda x_{n}.M)\dots))$
>- *Applicazione associa a sinistra*: $F N_{1} N_{2} ... N_{n}$ equivale a $(\dots(F N_{1}) \dots N_{n})$

## Computazione (β-regola)

La computazione avviene tramite la $\beta-\text{riduzione}$ (beta-regola): un termine della forma $(\lambda x.M )N$ si dice **b-redex** e si riduce sostituendo tutte le occorrenze di `x` in `M` con il termine `N` . Formalmente:

$$
(\lambda x.M )N \to_{\beta} M [N /x]
$$

Un termine che non contiene più $\beta \text{-redex}$ è detto in **forma normale** e rappresenta un valore finale (il risultato della computazione).

>[!note] Significato Redex
>
>Redex sta per **REDucible EXpression** (Espressione Riducibile). Quindi, un *β-redex* significa letteralmente: *"Un pezzo di codice che è pronto per essere calcolato tramite la regola beta"*.

## Variabili libere (free) e legate (bound)

**Variabile Legata (Bound):** È una variabile che compare nel corpo di una funzione _ed è stata dichiarata nella λ di quella funzione_. In programmazione, è un **parametro locale**.

**Variabile Libera (Free):** È una variabile che viene usata nel corpo, ma _non c'è nessun λ che la definisce_. In programmazione, è una **variabile globale** che arriva dall'esterno.

>[!example] Esempi
>
>Nel termine $\textcolor{orange}{x}(\lambda \textcolor{red}{x}.(\lambda y.y \textcolor{red}{x}))$ ho che:
>- la prima $\textcolor{orange}x$ è libera
>- mentre le `y` e le $\textcolor{red}{x}$ sono legate

>[!note] Barendregt Name Convention
>
>Osservare che nell'esempio precedente abbiamo lo stesso nome per due variabili diverse ($\textcolor{orange}x \neq \textcolor{red}x$).
>
>Infatti l termine $\textcolor{orange}{x}(\lambda \textcolor{red}{x}.(\lambda y.y \textcolor{red}{x}))$ è equivalente al termine $\textcolor{orange}{x}(\lambda \textcolor{green}{z}.(\lambda y.y \textcolor{green}{z}))$ e a tutti i termini in cui rinomino le variabili legate ($\alpha\text{-regola}$/$\alpha\text{-conversione}$).
>
>Per evitare problemi, possiamo assumere tutti i nomi delle variabili legate diversi tra loro e diversi da quelli delle variabili libere.

## Combinatori

I termini tali che ($F V (M ) = ∅$) (λ-termini chiusi), ovvero senza variabili libere, sono chiamati
combinatori.

Poiché nel λ-calcolo puro non esistono tipi di dato predefiniti, i combinatori vengono utilizzati per codificare ogni struttura logica e matematica, dai booleani ai numeri.

>[!note] Cancellatori (Bool)
>
>Nel λ-calcolo, un valore booleano è interpretato come una **funzione di scelta**:
>- $K$ (o $T$ per True): **$K \equiv \lambda tf.t$**, ovvero:  prende due argomenti e restituisce il primo (`KMN->M`)
>- $O$ (o $F$ per False) **$O \equiv \lambda tf.f$**, ovvero: prende due argomenti e restituisce il secondo (`OMN->N`)
>
>Proprio perché i booleani sono "selettori", il costrutto `if-then-else`è una semplice **applicazione di funzione**. L'espressione `if x then M else N` in lambda calcolo viene scritta semplicemente come `x M N`, infatti:
>1. Se `x` è **True** ($K$): L'espressione diventa `K M N`. Per definizione di `K`, il risultato è `M` (il ramo _then_).
>2. Se `x` è **False** ($O$) L'espressione diventa `O M N`. Per definizione di `O`, il risultato è `N` (il ramo _else_).

^163165

>[!note] Tuple
>
>>[!warning] nuple 
>>
>>Una tupla $(M_{1},M_{2}​,\dots,M_{k}​)$ è codificata come $\lambda x.xM_{1}​M_{2}​\dots M_{k}$​. 
>>
>>Per estrarre i valori si usano i **proiettori** $\pi^{k}_{j}​ \equiv \lambda x_{1}\dots x_{k}​.x_{j}$

### Numeri di Church e Iteratori

I Numerali di Church rappresentano i numeri naturali come funzioni di ordine superiore che iterano
un’operazione. 

Il numero `n` è una funzione che applica `n` volte un parametro `s` (successore) a una base `z` (zero): 

$$n \equiv \lambda sz.s(s(\dots(sz)\dots))\ \ \ [\text{n applicazioni}]$$

- $0 \equiv \lambda sz.z$ (equivale a [[#^163165|False]] ($K$))
- $1 \equiv \lambda sz.sz$
- $2 \equiv \lambda sz.s(s(z))$
- $3 \equiv \lambda sz.s(s(s(z)))$

>[!note] Successore
>
>Per calcolare il successore (`+1`) di un numero di Church, basta creare una funzione che applica `s` una volta in più: 
>$$succ \equiv \lambda x.\lambda sz.s(xsz)$$
>
>Scomponiamolo:
>1. **$\lambda xsz.$** : Questa funzione prende tre input. Prende il numero di partenza ($x$), l'azione da fare ($s$) e il punto di partenza ($z$).
>2. **$x\ s\ z$** : Qui stiamo "attivando" il numero $x$. Gli diamo la nostra azione $s$ e la base $z$. Essendo un numerale di Church, il numero $x$ eseguirà l'azione $s$ per $x$ volte partendo da $z$.
>3. **$s( \dots )$** : Infine, prendiamo il risultato di tutto quel lavoro (l'azione ripetuta $x$ volte) e gli applichiamo sopra l'azione $s$ **un'ultima volta** noi stessi.
>   
>>[!example] Esempio Computazione
>>
>>```
>>succ 3 
>>	≡ (λx.λsz.s(xsz)) 3 
>>	→ λsz.s(3sz) 
>>	≡ λsz.s(λxy.x(x(xy)) s z)  
>>	→ λsz.s(s(s(sz))) 
>>	≡ 4
>>```
>>
>>>***Nota:*** $3 \equiv \lambda xy.x(x(xy))$

>[!note] Altre Operazioni
>
>- [[Operazioni Numeri Church - Lambda Calcolo]]
## Cose

>[!note] Identità ($I$)
>
>$I \equiv \lambda x.x$, ovvero: qualsiasi termine applicato a `I` rimane invariato (`I M -> M`)
>

^c321b5

>[!note] Compositore ($S$):
> $S \equiv \lambda xyz.xz(yz)$ distribuisce l'argomento `z` sia alla funzione `x` che alla funzione `y`.
>
>Un notevole  utilizzo è `S K K` che si comporta esattamente come l'**identità** $I$ ($SKK \approx I$)
>
>---
>
>Per **dimostrare** che $SKK \approx I$, dobbiamo applicare un termine generico `w` a questa combinazione e vedere se otteniamo `w` come risultato:
>
>1. ***Espressione iniziale***: `(SKK) w`
>2. ***Applichiamo la definizione di S***: (dove x=K,y=K,z=w) `(SKK) w -> (K w)(K w)`.
>3. ***Applichiamo la definizione di K***: Ricorda che `K` applicato a un termine (in questo caso `w`) restituisce una funzione costante che ignora il suo secondo argomento e restituisce sempre quel termine.
>4. ***Calcolo finale:*** Nell'espressione `(K w)(K w)`, il primo `(K w)` agisce come una funzione che riceve il successivo `(K w)` come secondo argomento, quindi: `(K w)(K w) -> w`.

>[!note] Duplicatore $\omega$
>
>$\omega \equiv \lambda x.xx$ , ovvero l'operazione di *auto-applicazione*

>[!note] Combinatore $\Omega$
>
>Definito come $(\lambda x.xx)(\lambda x.xx)$ ovvero $\omega \omega$. Rappresenta il **loop infinito** per eccellenza perché riduce sempre a se stesso senza mai raggiungere una forma normale.
>
>$$
>\omega \omega \to  \omega \omega \to \dots
>$$
>
>**In Haskell**, $\Omega$ e l'auto-applicazione **non sono tipabili** a causa dell'occurs check, un controllo che impedisce la creazione di tipi infiniti.


### Combinatori per la Ricorsione (Punto Fisso)

Per definire funzioni ricorsive generali, il λ-calcolo utilizza il **Combinatore di Punto Fisso ($Y$)** , tale che $YM\to M(YM)$. I due più noti sono:

- **Combinatore di Turing ($YT$)**: Definito come $\theta\theta$ dove $\theta \equiv \lambda xy.y(xxy)$.
- **Combinatore di Curry ($YC$)**: Definito come $λf.(λx.f(xx))(λx.f(xx))$.

