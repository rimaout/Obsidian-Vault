---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2024-11-20T10:55
updated: 2024-11-20T11:13
---

>[!abstract] Related
>- 

---
## Introduzione

>[!note] Equivalenza tra due insiemi di dipendenze funzionali
>
>Siano $F$ e $G$ due insiemi di dipendenze funzionali. $F$ e $G$ sono equivalenti ($F \equiv G$) se $F^{+} \equiv G^{+}$
>
>**Ovvero:** $G$ e $F$ non sono uguali (non contengono le stesse dipendenze) ma hanno la stessa chiusura.
>
>>[!danger] Verificare l’equivalenza
>>Per verificarlo dobbiamo [[Calcolare chiusura di un insiemi di dipendenze funzionali|calcolare la chiusura]] la chiusura di $F$ e di $G$, ma questo metodo richiede tempo esponenziale quindi possiamo usare un metodo alternativo usando il [[#Lemma 2]] e il teorema $F^{+} = F^{A}$.

---
## Lemma 2

Siano $F$ e $G$ due insiemi di dipendenze funzionali. Se $F \subseteq G^{+}$ allora $F^{+} \subseteq G^{+}$.

>[!warning] Dimostrazione (da finire)
>Sia $f \in F^{+} - F$
>
>1. Visto che $F \subseteq G^{+}$ vol dire che tutte le dipendenza funzionali di $F$ possono sicuramente essere ottenute, applicando gli assiomi di Armstrong su $G$.
>2. 
>
>Ogni dipendenza funzionale in $F$ è derivabile da $G$ mediante gli assiomi di Armstrong (per l'ipotesi si trova $G^{+}$ e il teorema che abbiamo dimostrato afferma che $F^{+} = F^{A}$)
>
>Sempre il teorema che dimostra $F^{+} = F^{A}$, $f$  in $F^{+}$ è derivabile dalle dipendenze in $F$ mediante gli assiomi di Armstrong

Questo lemma insieme al teorema $F^{+} = F^{A}$ ci permette di calcolare $F^{+}$ semplicemente ...vjkjasvdjl
