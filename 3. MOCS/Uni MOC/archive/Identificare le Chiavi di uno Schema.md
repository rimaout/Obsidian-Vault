---
type: Uni Note
class:
  - "[[Basi di Dati 1 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2024-11-19T11:57
updated: 2026-01-31T13:32
---
## Verifica della Chiave

È possibile determinare se un sotto schema $X$ di uno schema razionale $R$  è [[Dipendenze Funzionali#Chiave|chiave]] utilizzando il calcolo della [[Chiusura di un Insieme di Attributi]].

>[!note] Metodo
>Prima di tutto dobbiamo dimostrare che il sotto schema $X$ è almeno una [[Dipendenze Funzionali#^12345|super-chiave]], ovvero che raggiunge tutto $R$.
>
>Per fare ciò calcoliamo la chiusura $X^{+}$ di $X$ e verifichiamo che sia uguale a $R$.
>
>Fatto ciò dobbiamo verificare che $X$ si una chiave (minimale) ovvero che non esista un suo sotto insieme che è a sua volta chiave.
>
>Per fare ciò dobbiamo calcolare la chiusura dei sottoinsiemi di $X$ e se nessuna di queste è uguale ad $R$ abbiamo dimostrate che $X$ è una chiave minimale.
>
>Per rendere il procedimento più rapito si possono seguire questi [[#^c95a08|consigli]].

^701285

>[!warning] Consigli
>
>1. Un attributo che non compare mai come dipendente (a destra) sarà sicuramente parte di tutte le chiavi.
>2. Un attributo che compare sempre come dipendente (a destra) non farà parte delle chiavi.
>3. Per verificare se una super-chiave è anche una chiave, è necessario controllare che nessuno dei suoi sottoinsiemi sia una chiave. Un modo efficiente per farlo è partire dai sottoinsiemi più grandi e verificare se la loro chiusura contiene tutti gli attributi. Se non è così, si può escludere che il sottoinsieme sia una chiave e non è necessario proseguire con i suoi sottoinsiemi.

^c95a08

>[!example]- Esempio
>**Schema Relazionale:** $R = \{ A,\,B,\,C,\,D,\,E,\,H \}$
>**Dipendesse Funzionali:** $F = \{ AB\to CD,\ C \to E,\ AB \to E,\ ABC \to D \}$
>
>***Determinare:*** se $ABH$ è una chiave
>
>Calcoliamo la chiusura di $ABH$:
>1. $ABH \to CD$ (per $AB \to CD$) 
>2. $ABCDH \to C$ (per $C \to E$)
>
>Abbiamo che:
>$$
>ABH^{+} = ABCDEH = R
>$$
>
>Quindi abbiamo verificando che $ABH$ è una super chiave dimostrando che la chiusura di $ABH^{+}$ è uguale ad $R$.
>
>Ora dobbiamo verificare che $ABH$ sia una chiave (minimale), per fare ciò calcoliamo la chiusura dei sui sotto insieme seguendo i [[#^701285|consigli]] visti.
>
>Per prima cosa dobbiamo tenere conte che $H$ va sicuramente nella chiave dato che non viene mai determinato e quindi dobbiamo controllare i sottoinsiemi $AH$, $BH$ che sono quelli di cardinalità più grande.
>
>Calcolando la chiusura di entrambi i sottoinsiemi ci accorgiamo che non determinano altri attributi quindi possiamo fermarci qui, è inutile controllare sottoinsiemi di cardinalità inferiore, quindi $ABH$ è chiave.

^8f8034


---
## Trovare tutte le Chiavi

Per trovare tutte le chiavi di un schema relazionale possiamo utilizzare questi [[#^c95a08|consigli]] per identificare quali attributi fanno e non fanno sicuramente parte delle chiavi.
Poi testare tutte le possibili combinazioni di attributi utilizzando il [[#^701285|metodo]] visto precedentemente.

Naturalmente conviene iniziare dalle combinazioni più piccole infatti se trova una chiave, puoi escludere tutte le combinazioni più grandi che includono quella chiave.

>[!example]- Esempio
>
>Continuiamo l'[[#^8f8034|esempio precedente]].
>
>Abbiamo detto che `H` deve essere sicuramente parte della chiave e abbiamo già verificato che `H`,`AH`,`BH` non sono chiavi, proviamo a controllare `CH`,`DH`,`EH`.
>
>- `CH -→ CHE` quindi non è chiave.
>- `DH -→ DH` quindi non è chiave
>- `EH -→ EH` quindi non è chiave
>
>Quindi ci restano da testare soltanto 3 attributi: `H` che abbiamo fisto che fa sicuramente parte della chiave, `A` e `B` che non abbiamo testato a parte per `ABH`.
>
>Notiamo che `A` e `B` da soli non determinano nulla e inoltre non dipendono da altri attributi quindi vanno per forza nella chiave. Questo significa che ABH è l’unica chiave.

>[!note] Metodo Alternativo
>
>Alternativamente si può cominciare dagli insiemi individuati dalle dipendenze funzionali ovvero:
>
 Data una dipendenza $V\to W\in F$ calcoliamo la chiusura dell’insieme di attributi $X=R−(W−V)$. 
>
>Se la chiusura di questo insieme $X$  contiene $R$  allora $X$  è [[Dipendenze Funzionali#^12345|super-chiave]], (serve verificare che sia una [[Dipendenze Funzionali#Chiave|chiave]] minimale).
>
>>[!example]- Esempio
>>
>>Calcolare le chiavi di:
>>
>>**Schema Relazionale:** $R = \{ A,\,B,\,C,\,D,\,E \}$
>>**Dipendesse Funzionali:** $F = \{ AB\to C,\ AC \to B,\ D \to E \}$
>>
>>Quindi in base a quanto detto prima calcoliamo le super-chiavi:
>>
>>$$
>>\begin{align*}
>>& ABCDE - (C-AB) = (ABDE)^{+} = R\\
>>& ABCDE - (B-AC) = (ACDE)^{+} = R\\
>>& ABCDE - (E-D) = (ABCD)^{+} = R\\
>>\end{align*}
>>$$
>>
>>Adesso però dobbiamo verificare che siano chiavi.
>>
>>Notiamo che:
>>- $A$, $D$ vanno sicuramente nella chiave
>>- $A$ da solo non determina nulla quindi va sicuramente insieme a $C$ o $B$.
>>  
>>Quindi proviamo a verificare $ADC$ e $ADB$:
>>$$
>>\begin{align*}
>>&ADC \to  BE\ \text{ è chiave}\\
>>&ADB \to  CE\ \text{ è chiave}
>>\end{align*}
>>$$
>>
>>Quindi $$ABDE$$ e $$ABCD$$ non sono chiavi minimali dato che contengono $ABD$ mentre $ACDE$ non è chiave dato che contiene $ADC$.
>>
>>Per [[#^c95a08|queste osservazioni]], inutile controllare sottoinsiemi di $ABD$ e $ADC$ dato che dobbiamo avere sicuramente D e A non può stare da solo.
>>

^0aed0f

>[!note] Test Unicità
>
>Tecnica che ci permette determinare se uno schema relazionale ha 1 o più chiavi.
>
>Calcoliamo l'intersezione di tutti gli insiemi $X$ ottenuti con la [[#^0aed0f|formula di prima]] e chiamiamo l'insieme $Y$ effettuiamo la chiusura di $Y$. 
>
>- Se il risultato della chiusura è $R$ allora $Y$ è l'unica chiave, altrimenti c'è più di una chiave in $R$.
>
>>[!example]- Esempio
>>
>>Calcoliamo la chiusura dell’intersezione degli insiemi ottenuti con la formula di prima, nell'[[#^0aed0f|esempio precedente]]:
>>
>>$$
>>(ABDE \cap ACDE \cap ABCD)^{+} = (AD)^{+} = AD
>>$$
>>
>>Quindi essendo $AD \not=R$  sabbiamo che in $R$ c'è più di una chiave.

