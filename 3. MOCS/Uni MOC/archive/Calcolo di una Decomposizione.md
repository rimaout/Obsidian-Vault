---
type: Uni Note
class: "[[Basi di Dati 1 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2024-11-25T09:41
updated: 2026-01-31T13:32
---
## Introduzione

Come abbiamo visto una [[Decomposizione di uno schema relazionale|decomposizione]] deve rispettare queste 3 condizioni:
1. Ogni *sotto-schema* deve essere *3NF*
2. La decomposizione deve *preservare le dipendenze funzionali*
3. Deve essere possibile ricostruire ogni istanza legale dello schema originale tramite join naturale di istanze della decomposizione

Abbiamo anche visto come [[Decomposizione con Join senza Perdita (Verifica)|verificare]] che una decomposizione rispetti queste regole, ma non abbiamo ancora visto come calcolare una decomposizione valida.

>[!question] Sempre possibile ?
>**Si**, è sempre possibile trovare una decomposizione valida.

---
## Algoritmo 

La decomposizione che si ottiene dall’algoritmo che studieremo non è l’unica possibile che soddisfi le condizioni richieste. Lo stesso algoritmo, a seconda dell’input di partenza può fornire risultati diversi e tuttavia corretti.

Prima di continuare è importante conoscere il concetto di [[Copertura Minimale|copertura minimale]] di un insieme $F$ di dipendenze funzionali.

$$
\begin{align*}
&S:=\varnothing \\
&\mathbf{for\,\,every} A\in R\text{ tale che }A\text{ non è coinvolto in nessuna dipendenza funzionale in F} \\
&\qquad S:=S\cup \{A\} \\\\
&\mathbf{if\,\,}S\neq \varnothing\mathbf{\,\,then} \\
&\qquad R:=R-S \\
&\qquad \rho:=\rho \cup \{S\} \\ \\
&\mathbf{if}\text{ esiste una dipendenza funzionale in }F\text{ che coinvolge tutti gli attributi in }R \\
&\qquad\rho:=\rho \cup \{R\} \\ \\
&\mathbf{else}\ \; \mathbf{for\,\,every\,\,}X\to A \\
&\qquad\qquad \rho:=\rho \cup \{XA\} \\
\end{align*}
$$

>[!note] Input/Output
>
>***Input:***
>- uno schema relazionale $R$ 
>- un insieme di dipendenze funzionali $F$ che è una copertura minimale (se abbiamo più coperture è consigliato utilizzare quella con il minor numero di dipendeze)
>
>***Output*** una decomposizione $\rho = \{ R_{1},\, R_{2},\dots,\,R_{k}  \}$ di $R$ tale che: 
>- ogni schema relazionale in $\rho$ è in [[Terza Forma Normale (3NF)|3NF]]
>- $\rho$ preserva $F$
>- $\rho$ ha un [[Decomposizione con Join senza Perdita (Verifica)|join senza perdita]]

>[!warning] Spiegazione
>***Primo FOR:*** inserisce dentro $S$ tutti gli attributi che non compaiono in nessuna delle dipendenze funzionali di $F$.
>
>***Primo IF:*** Se $S$ non è vuoto allora
>- Rimuoviamo da $R$ tutti gli attributi che non compaiono mai nelle dipendenze di $F$ (ovvero facciamo $R-S$)
>- Inseriamo in $\rho$ l'insieme di attributi $S$ (quindi avremo che $\rho = \{ \{ S \} \}$)
>  
>***Secondo IF:*** se 
>
>***else:***
>
>>**oss:** l’algoritmo richiede tempo polinomiale

---
## Dimostrazione 

Abbiamo dette che questo algoritmo ci permette di ottenere un decomposizione che rispetta queste due proprietà:
- Ogni *sotto-schema* deve essere *3NF*
- La decomposizione deve *preservare le dipendenze funzionali*

Dimostriamolooo!! 😖

>[!note] Dimostrazione: ogni sotto-schema deve essere 3NF
>Ci sono 3 modi per aggiungere degli insiemi di attributi:
>- `1°  if:` $\rho = \rho \cup \{ S \}$
>- `2° if:` $\rho = \rho \cup \{ R \}$
>- `if else:` $\rho = \rho \cup XA$
>  
>---
>***1° IF***
>
>Eseguiamo $\rho = \rho \cup \{ S \}$ ovvero aggiungiamo a $\rho$ l'insieme degli attributi non coinvolti in alcuna dipendenza dipendenze di $F$.
>
>Banalmente $S$ è in 3NF perché sicuramente ogni attributo in $S$ appartiene alla chiave visto che non esistono dipendenze in $F$ per raggiungerli.
>
>---
>***2° IF***
>
>Eseguiamo $\rho = \rho \cup \{ R \}$ ovvero aggiungiamo ad $\rho$ l’insieme degli attributi coinvolti nelle dipendenze di $F$.
>
>*oss:* al passaggio precedente abbiamo effettuato $R = R - S$ quindi $R$ non contiene gli attributi che non sono coinvolti nelle dipendenze di $F$.
>
>

---
## Teorema

Sia $R$ uno schema di relazione ed $F$ un insieme di dipendenze funzionali su $R$, che è una copertura minimale. L’algoritmo di decomposizione permette di calcolare in tempo polinomiale una decomposizione $\rho$ di $R$ tale che:
- ogni schema di relazione $\rho$ è in 3NF
- $\rho$ preserva $F$

>[!info] Dimostrazione
>Dimostriamo separatamente le due proprietà della decomposizione
>
>##### $\rho$ preserva $F$
>Sia $G=\cup_{i=1}^k \pi_{R_{i}}(F)$. Poiché per ogni dipendenza funzionale $X\to A\in F$ si ha che $XA\in \rho$ (è proprio uno dei sottoschemi), si ah che questa dipendenza di $F$ sarà sicuramente in $G$, quindi $F\subseteq G$ e, quindi $F^+\subseteq G^+$. L’inclusione $G^+\subseteq F^+$ è banalmente verificata in quanto per definizione, $G\subseteq F^+$