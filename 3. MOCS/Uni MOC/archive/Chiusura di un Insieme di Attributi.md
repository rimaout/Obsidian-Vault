---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2024-11-16T17:24
updated: 2024-11-27T10:34
---
>[!abstract] Related
>- 

---
## Introduzione

Quando si [[Decomposizione di uno schema relazionale|decompone]] uno schema `R` su cui è definito un insieme di dipendenze funzionali `F` per ottenere altri schemi in [[Terza Forma Normale (3NF)|3NF]], è importante preservare tutte le dipendenze in $F^{+}$.

Quindi ci serve calcolare $F^{+}$, però questo procedimento può essere lungo visto che richiede tempo esponenziale rispetto alla cardinalità di `R` (${ \lvert R \rvert }$).

In realtà ci basta sapere se una dipendenza funzionale $X \to Y$ appartiene ad $F^{+}$, e possiamo farlo calcolando $X^{+}$ e verificando che $Y\subseteq X^{+}$, infatti per il lemma 1: $\ X \to Y \in F^{A} \iff Y \subseteq X^{+}$ e poi il teorema dimostra che $F^{A}=F^{+}$.

Inoltre il calcolo di $X^{+}$ può tornare utile per verificare che un insieme di attributi sia chiave di uno schema.

---
## Calcolo Chiusura (Algo)

Il calcolo della chiusura di un insieme di attributi $X$ denotato come $X^{+}$ può essere fatto attraverso questo algoritmo.

$$
\begin{flalign*}
&Z:=X\\
&S:=\{A \mid Y\to V\in F,\,\, A\in V,\,\, Y\subseteq Z\}\\ \\
&\text{while } S\not\subset Z:\\
&\qquad\qquad Z:=Z\cup S\\
&\qquad\qquad S:=\{A \mid Y\to V\in F,\,\, A\in V,\,\, Y\subseteq Z\}\\

\end{flalign*}
$$

>[!warning] Input
>- `R:`Schema relazionale
>- `F:`Insieme di dipendenze funzionali su $R$
>- `X:`Un sottoinsieme di $R$

>[!warning] Output
>- `Z:` Chiusura di $X$ rispetto ad $F$

>[!info] Approfondimento
>Inizialmente abbiamo che: 
>- $Z$ che è uguale ad $X$ 
>- $S$ contiene i singoli attributi che compongono le parti a destra delle dipendenze funzionali la cui parte sinistra è in $Z$.
>  
>Quindi inizialmente in $S$  avremo gli attributi determinati da $X$ . 
>  
>Poi aggiungiamo questi elementi a $Z$  e continuiamo a iterare sui nuovi insieme $Z$ .
>
>Ci fermiamo quando $S$ non ha elementi “nuovi” rispetto a $Z$ .

---
## Esempi

***Aggiungere Esempi Migliori***

>[!example] Esempio 1 
>![[Pasted image 20241119114652.png]]
>
>Notiamo che per ogni passaggio dobbiamo sempre far partire la catena di operazioni da $AB$ .
>
>È quindi più semplice vedere cosa abbiamo in $Z$  e “combinando” i pezzi vedere cosa possiamo ottenere.
>
>Adesso dobbiamo dimostrare che l’algoritmo è corretto, ovvero che calcola correttamente la chiusura di un insieme di attributi $X$  rispetto ad un insieme $F$  di dipendenze funzionali.

---
## Dimostrazione

***Aggiungi dimostrazioneeeeeee***