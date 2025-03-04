---
type: Uni Note
class:
  - "[[Basi di Dati 2 (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2025-03-03T19:29
updated: 2025-03-03T19:29
---
## Fasi

È possibile suddividere lo sviluppo di un software in 8 macro-fasi principali:

**1) Studio di Fattibilità** - In questa fase si devono comprendere i requisiti ad alto livello, valutare i costi pianificare le attività/risorse del progetto e individuare l'ambiente di programmazione (hardware/software)

**2) Raccolta dei Requisiti** - In questa fase si richiedono i requisiti presso i vari attori, viene stesa una sintesi iniziale e poi approfondimento dei requisiti.

**3) Analisi concettuale dei Requisiti** - Viene prodotto lo schema concettuale dell'applicazione, che definisca in dettaglio `cosa` l’applicazione dovrà realizzare, indipendentemente dal `come`.

>[!note] Schema concettuale
>Lo schema concettuale è un modello logico-matematico dell’applicazione, e sarà la base da cui partire per le successive attività di progettazione (*è matematico perché le parole possono essere ambigue la matematica no*)
>- Modella i dati di interesse, le loro articolazioni, interrelazioni ed evoluzioni possibili
>- Specifica i servizi computazionali che l'applicazione dovrà offrire ai diversi utenti

**4) Progetto (design) dell'applicazione** - Viene specificato `come` l’applicazione dovrà realizzare le sue funzioni, ovvero viene definita la struttura del progetto e vengono scelte le tecnologie e le strutture dati utilizzate.

**5) Realizzazione (implementazione) dell’applicazione** -  Consiste nella *scrittura il codice* e della documentazione.

**6) Integrazione dei componenti e verifica dell’applicazione** - Le diverse componenti dell’applicazione, sviluppate separatamente, vengono integrate e si valuta se l’applicazione svolge correttamente, completamente ed efficientemente i suoi compiti.

**7) Messa in esercizio dell’applicazione** - L’applicazione viene messa in esercizio ed inizia a funzionare.

**8) Manutenzione dell’applicazione** - L’applicazione viene monitorata durante l’esercizio e correzioni ed aggiornamenti vengono prodotti se necessari.

### Metodo

Solitamente in situazione accademica e didattica si utilizza il modello a **cascata** (waterfall model) dove ogni attività inizia quando termina quella precedente.

Nel mondo reale si utilizza un modello a **spirale** anche detto iterativo. Questo modello permette di partire da versioni più semplice e "agili"  che poi man mano diventano sempre più complessi e vicine all'obbiettivo finale.

Questo permette di eseguire varie fasi in parallelo, ad esempio, nel tempo `t0` vengono stilati i requisiti per la prima versione del software, nel tempo `t1` gli analisti iniziano a produrre il modello della versione `1`, ma possono essere nel mentre stilati i requisiti della versione `2`, al tempo `t3` si raccolgono i requisiti per la versione `3`, si produce il modello della versione `2`, si progetta la versione `1`.

![[Pasted image 20250227100427.png|700]]

>Schema preso dagli appunti di [@CasuFrost](https://github.com/CasuFrost/University_notes)


