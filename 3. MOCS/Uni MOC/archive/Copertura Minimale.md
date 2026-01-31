---
type: Uni Note
class: "[[Basi di Dati 1 (class)]]"
academic year: 2024/2025
related:
  - "[[Calcolo di una Decomposizione]]"
completed: true
created: 2024-11-25T09:40
updated: 2026-01-31T13:32
---
>[!abstract] Related
>- [[Calcolo di una Decomposizione]]
>- [[Basi di Dati 1 (class)]]

---
## Introduzione

Una copertura minimale è un insieme di dipendenze funzionali che è equivalente all'insieme originale di dipendenze funzionali, ma con il minimo numero di dipendenze funzionali necessarie per descrivere le relazioni tra gli attributi.

>***oss:*** Un insieme di dipendenze funzionali $F$, può avere più coperture minimali equivalenti. È proprio questo il motivo per cui l’[[Calcolo di una Decomposizione#Algoritmo|algoritmo di decomposizione]] può produrre risultati diversi, ma tutti corretti.

---
## Definizione

Sia $F$ un insieme di dipendenze funzionali. Una *copertura minimale* di $F$ è un insieme $G$ di dipendenze funzionali equivalente ad $F$ che rispetta queste 3 condizioni:

>[!note] Condizione 1
>
>Per ogni dipendenza funzionale in $G$ la parte destra è un singleton. 
>
>>***Importante:*** ogni attributo nella parte destra è non ridondante

>[!note] Condizione 2
>Per nessuna dipendenza funzionale $X\to A$ in $G$ esiste $X’\subset X$ tale che 
>
>$$
>G\equiv (G - \{ X \to A \}) \cup \{ X'\to A \}
>$$ 
>
>Ovvero non accedere che:
>- se a $G$ tolgo $X \to A$ e aggiungo $X'\to A$ 
>- dopo queste operazioni $G$ è restato invariato allora $X \to A$
>  
>>***Importante:*** ogni attributo nella parte sinistra è non ridondante

>[!note] Condizione 3
>Per nessuna dipendenza funzionale $X\to A$ in $G$ si ha che: 
>
>$$
>G\equiv G-\{ X \to A \}
>$$ 
>
>
>**Ovvero:** se a $G$ tolgo la dipendenza $X\to A$ e il "significato" di $G$ resta invariato allora $X \to A$ non va bene.
>  
>>***Importante:*** ogni dipendenza è non ridondante

---
## Calcolo

Per ogni insieme di dipendenze funzionali $F$ esiste una copertura minimale equivalente ad $F$ che può essere ottenuta in tempo polinomiale in tre passi:

>[!note] Passo 1
>Usando la regola della decomposizione, le parti destre delle dipendenze funzionali vengono ridotte a singleton.
>
>**Ovvero:** $A\to BC$ uguale ad $A \to B$ e $A \to C$

>[!note] Passo 2
>Ogni dipendenza funzionale $A_{1} \dots A_{i}A_{i+1}\dots A_{n} \to A$ in $F$ tale che:
>
>$$
>F \equiv F - \{  A_{1} \dots A_{i-1}\textcolor{orange}{A_{i}}A_{i+1}\dots A_{n} \to A \} \cup \{  A_{1} \dots A_{i-1}A_{i+1}\dots A_{n} \to A \}
>$$
>
>Deve essere sostituita da $A_{1}\dots A_{i-1}A_{i+1}\dots A_{n} \to A$, se quest’ultima appartiene già ad $F$  la dipendenza originaria viene semplicemente eliminata, altrimenti il processo viene ripetuto ricorsivamente su $A_{1}\dots A_{i-1}A_{i+1}\dots A_{n} \equiv A$
>
>Il passo termina quando nessuna dipendenza funzionale può più essere ridotta.

^0fdd51

>[!note] Passo 3
>
>Ogni dipendenza funzionale $X \equiv A$ in $F$ tale che:
>$$
>F \equiv  F - \{ X \to  A \}
>$$
>
>viene eliminata, in quanto risulta ridondante.

^9b2daa

---
## Verificare l'equivalenza $\equiv$

Il [[#^0fdd51|passo 2]] ed il [[#^9b2daa|passo 3]] richiedono la [[Lemma 2 - Basi di Dati 1|verifica dell'equivalenza tra due insiemi di dipendenze funzionali (Lemma 2)]].

Visto che ci troviamo in condizioni speciali vedremo che ci sono dei metodi semplificati per verificare l'equivalenza.

>[!note] Verifica $\equiv$ in passo 2
>
>Assumiamo che:
>- `F` sia l’insieme di dipendenze funzionali
>- `G` sia l’insieme di dipendenze funzionali "ridotto"
>  
>  Notiamo che i due insieme sono identici tranne per una dipendenza
>- `F` conterrà la dipendenza "originale" che chiameremo $X\to A$
>- `F` conterrà la dipendenza "ridotta" che chiameremo $X'\to A$
>  
>>***oss:*** $X' \subset X$
>  
>  Per verificare l’equivalenza tra `F` e `G` dobbiamo solo controllare che 
>  - la dipendenza "originale" ($X\to A)$ si trovi in $G^{+}$
>  - la dipendenza "ridotta" ($X'\to A)$ si trovi in $F^{+}$.
>    
>>***oss:*** non serve ricalcolare la chiusura di attributi di cui l'abbiamo già calcolata (non cambiano)
>
>>[!example]- Esempio
>>$F = \{ AB \to C,\ A \to D,\ D \to C \}$
>>
>>**Verifichiamo:** se è possibile rimuovere la $B$ da $AB \to C$, abbiamo che $\ G = \{ A \to C,\ A \to D,\ D \to C \}$
>>
>>Quindi dobbiamo verificare che:
>>- $A \to C \in F^{+}$ 
>>- $AB \to C \in G^{+}$
>>
>>Per verificare che $A \to C \in F^{+}$ possiamo l'[[Chiusura di un Insieme di Attributi#Calcolo Chiusura (Algoritmo)|algoritmo per il calcolo della chiusura di un insieme di attributi]] inizializzando l'input $Z$ ad $Z = A$ e si applicando le dipendenze in $F$.
>>- una volta applicato l’algoritmo notiamo che $C\in A^{+}_{F}​$ ✅
>>
>>Per verificare che $AB \to C \in G^{+}$ possiamo l'[[Chiusura di un Insieme di Attributi#Calcolo Chiusura (Algoritmo)|algoritmo per il calcolo della chiusura di un insieme di attributi]] inizializzando l'input $Z$ ad $Z = AB$ e si applicando le dipendenze in $G$.
>>- Questo caso è molto banale infatti abbiamo che $G$ contiene $A \to C$ quindi è ovvio che $AB \to C$. ✅

>[!note] Verifica $\equiv$ in passo 3
>Assumiamo che:
>- `F` sia l'insieme delle dipendenze funzionali che contiene la dipendenza $X\to A$
>- `G` sia uguale ad $F$ ma $X\to A$ è stata rimossa
>  
>>***oss:*** Notiamo che i due insieme differiscono soltanto per una dipendenza e che $G \subset F$ quindi $G^{+} \subseteq F^{+}$
>
>Quindi per verificare che $F \equiv G$ ci resta soltanto da controllare che $F^{+} \subseteq G^{+}$, che sarà sicuramente vero se $F \subseteq G^{+}$
>
>Ma visto che $F$ e $G$ differiscono soltanto per $X \to A$ e basta verificare che $X \to A \in G^{+}$ ovvero che $A \in (X)^{+}_{\ \ G}$
>
>>***oss:*** serve ricalcolare la chiusura di attributi di cui l'abbiamo già calcolata, infatti potrebbe cambiare

---
## Esempi

**Vedi altri esercizi [[3. MOCS/Uni MOC/archive/attachments/20. Algoritmo di decomposizione - Esercizi.pdf|qui]]**

>[!example] Esempio
>***Calcolare la copertura minimale di:***
>$$
>R = (A,B,C,D,E,H)
>$$
>
>$$
>F = \{ AB \to CD,\ C \to E\ AB \to E,\ ABC \to D  \}
>$$
>
>![[3. MOCS/Uni MOC/archive/attachments/Pasted image 20241127110630.png|900]]
>
>![[3. MOCS/Uni MOC/archive/attachments/Pasted image 20241127110656.png|1100]]
>
>![[3. MOCS/Uni MOC/archive/attachments/Pasted image 20241127110712.png|1100]]
