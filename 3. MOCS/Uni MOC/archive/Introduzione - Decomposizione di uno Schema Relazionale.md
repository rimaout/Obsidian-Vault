---
type: Uni Note
class:
  - "[[Basi di Dati 1 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2024-11-20T11:42
updated: 2026-01-31T13:32
---

## Introduzione 

Una decomposizione di uno schema relazionale è un processo che consiste nel suddividere uno schema relazionale in più schemi più piccoli e indipendenti, mantenendo le relazioni tra di loro.

Si può scomporre una relazione per diversi motivi solitamente si gli obbiettivi ridurre la complessità dello schema originale, migliorando la gestione dei dati e riducendo la ridondanza.

>[!info] 3NF
>Abbiamo visto che uno schema in [[Terza Forma Normale (3NF)|3NF]] ha delle buone proprietà che lo rendono preferibile ad uno che non è in 3NF.
>
>Quando si progetta una base di dati è importante di produrre uno schema in cui ogni relazione sia in 3NF. Se tuttavia ci trovassimo a produrre uno schema che non è in 3NF dovremmo procedere ad una fase di decomposizione, dove ***suddividiamo*** lo schema *non 3NF* in un *insiemi di schemi 3NF*.
>

>[!note] Definizione di Decomposizione
>Sia $R$ uno schema di relazione. Una ***decomposizione*** di $R$ è una famiglia $\rho = \{ R_{1}, R_{2} , \dots, R_{k}\}$ di *sottoinsiemi* di $R$ che ricopre $R ( \cup_{i=1^{k}} \ R_{i} = R)$
>
>**In altre parole:** 
>- Decomporre lo schema $R$ significa definire dei sottoschemi che contengono ognuno un sottoinsieme degli attributi di $R$. I sottoschemi possono avere attributi in comune, e la loro unione deve necessariamente contenere tutti gli attributi di $R$.
>- Quindi $R$ è un insieme di attributi, una decomposizione di $R$ è una famiglia di insiemi di attributi.

---
## Decomposizione di uno schema 3NF

Uno schema non in 3NF può essere **decomposto** in **più modi** in un insieme di schemi 3NF, ma non detto che tutti questi schemi siano egualmente validi.

>[!note] Regole
>Quando si decompone uno schema per ottenere una 3NF dobbiamo ricordare che:
>1. Occorre **preservare le [[Dipendenze Funzionali]] $F^{+}$** che valgono sullo schema originario.
>2. Occorre permettere di **ricostruire tramite join** lo schema originario, senza aggiunta di informazioni estranee.
 
>[!example]- Esempio 1
>**Schema relazionale:** $R = ABC$
>**[[Dipendenze Funzionali]]:** $F = \{ A \to B, B\to C \}$
>
>Questo schema non è in 3NF per via della dipendenza transitiva `B -> C` dato che la chiave è `A`. 
>
>È possibile decomporre questo schema in due modi tali che rispettano entrambi le condizione per essere 3NF:
>
>**Decomposizione 1:**
>- $R_{1} = AB$ con $\{ A \to B \}$
>- $R_{2} = BC$ con $\{ B \to C \}$
>
>**Decomposizione 2:**
>- $R_{1} = AB$ con $\{ A \to B \}$
>- $R_{2} = AC$ con $\{ A \to C \}$
>
>Entrambi gli schemi sono in 3NF, tuttavia la *2° soluzione non va bene*, perché?
>
>Consideriamo le istanze legali ottenute e li loro [[Join-Naturale e Theta-Join (Algebra Relazionale)#Join Naturale|join naturale]]:
>
>![[Pasted image 20241116122431.png|650]]
>
>Come possiamo notare il join naturale non è un istanza legale di $R$ perché non rispetta la dipendenza $B \to C$, *infatti dobbiamo preservare tutte le dipendenze presenti in $F^{+}$*.

>[!example]- Esempio 2
>**Schema relazionale:** $R = ABC$
>**[[Dipendenze Funzionali]]:** $F = \{ A \to B, C\to B \}$
>
>Questo schema non è in 3NF dato che entrambe le dipendenze sono parziali, la chiave è `AC`.
>
>È possibile decomporre questo schema in:
>
>- $R_{1} = AB$ con $\{ A \to B \}$
>- $R_{2} = BC$ con $\{ C \to B \}$
>
>Entrambe le istanze sono in 3NF, e rispettano tutte le dipendenze di $F^{+}$ ma non va comunque bene, infatti:
>
>Pendiamo un’istanza legale di R:
>![[Pasted image 20241116152511.png|130]]
>
>Decomponiamola in base ai due schemi visti prima:
>![[Pasted image 20241116152541.png|300]]
>
>In teoria facendo un join dovremmo ricostruire l’istanza originale ma non è così:
>![[Pasted image 20241116152829.png|320]]
>
>Le ultime due tuple sono estranee all’istanza originale, c’è stata quindi **perdita di informazione**.
