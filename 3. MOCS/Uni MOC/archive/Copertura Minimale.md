---
type: Uni Note
class: "[[Basi di Dati 1 (class)]]"
academic year: 2024/2025
related: 
completed: false
created: 2024-11-25T09:40
updated: 2024-11-26T13:09
---
>[!abstract] Related
>- 

---
## Introduzione

***copertura minimale*** di un insieme $F$  di dipendenze
funzionali.


>[!warning] oss
>
>un insieme di dipendenze funzionali $F$, può avere più coperture minimali equivalenti (nel senso di avere tutte la stessa chiusura, che poi è uguale anche a quella di F)
>
>È proprio questo il motivo per cui l’algoritmo di decomposizione può produrre risultati diversi, ma tutti corretti

---
## Definizione

Sia $F$  un insieme di dipendenze funzionali.

Una *copertura minimale* di $F$ è un insieme $G$ di dipendenze funzionali equivalente ad $F$ che rispetta queste 3 condizioni:

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
>Ovvero:
>- se a $G$ tolgo la dipendenza $X\to A$ e il "significato" di $G$ resta invariato allora $X \to A$ non va bene.
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
>Il passo termina quando nessuna dipendenza funzionale può più essere ridotta, quando tutti gli attributi delle parti sinistre delle dipendenze funzionali risultano non ridondanti.

>[!note] Passo 3
>
>
