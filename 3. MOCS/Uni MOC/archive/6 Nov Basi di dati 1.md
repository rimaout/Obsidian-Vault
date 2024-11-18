---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2024-11-06T15:21
updated: 2024-11-13T16:13
---
>[!abstract] Related
>- 

---
## Introduzione



---
## Definizione di Decomposizione

Sia $R$ uno schema di relazione. Una **decomposizione** di $R$ è una famiglia $\rho = \{ R_{1}, R_{2} , \dots, R_{k}\}$ di *sottoinsiemi* di $R$ che ricopre $R ( \cup_{i=1^{k}} \ R_{i} = R)$

**In altre parole:** 
- Se lo schema $R$ è composto da un certo insieme di attributi, decomporlo significa definire dei sottoschemi che contengono ognuno un sottoinsieme degli attributi di $R$. I sottoschemi possono avere attributi in comune, e la loro unione deve necessariamente contenere tutti gli attributi di $R$.
- Quindi: $R$ è un insieme di attributi, una decomposizione di $R$ è una famiglia di insiemi di attributi

***Esempio slide 11 due volte lo stessa persona che segue due corsi di laurea diversi***

---
## Equivalenza tra due insiemi di dipendenze funzionali


Siano $F$ e $G$ due insiemi di dipendenze funzionali. $F$ e $G$ sono equivalenti ($F \equiv G$) se $F^{+} \equiv G^{+}$

**Ovvero:** $G$ e $F$ non sono uguali (non contengono le stesse dipendenze) ma hanno la stessa chiusura.

>[!danger] Verificare l’equivaleza
>
>daljndkajdk
>
>Questo metodo richiede tempo esponenziale quindi possiamo usare un metodo alternativo usando [[#Lemma (2)]].

---
## Lemma (2)

Siano $F$ e $G$ due insiemi di dipendenze funzionali. Se $F \subseteq G^{+}$ allora $F^{+} \subseteq G^{+}$.

>[!warning] Dimostrazione
>Sia $f \in F^{+} - F$
>
>1. Visto che $F \subseteq G^{+}$ vol dire che tutte le dipendenza funzionali di $F$ possono sicuramente essere ottenute, applicando gli assiomi di Armstrong su $G$.
>2. 
>
>Ogni dipendenza funzionale in $F$ è derivabile da $G$ mediante gli assiomi di Armstrong (per l'ipotesi si trova $G^{+}$ e il teorema che abbiamo dimostrato afferma che $F^{+} = F^{A}$)
>
>Sempre il teorema che dimostra $F^{+} = F^{A}$, $f$  in $F^{+}$ è derivabile dalle dipendenze in $F$ mediante gli assiomi di Armstrong

Questo lemma insieme al teorema $F^{+} = F^{A}$ ci permette di calcolare $F^{+}$ semplicemente ...vjkjasvdjl

## ### Definizione FORMALE di uno schema relazionale

Sia $R$ uno schema di relazione, $F$ un insieme di dipendenze funzionali su $R$ e $\rho  = \{ R_{1}, R_{2}, \dots, R_{k} \}$ una decomposizione di $R$-

Diciamo che $\rho$ preserva $F$ se:
$$F \equiv \cup_{i=1^{k}}\ \pi_{Ri}(F)$$
Dove:
$$
\pi_{Ri} (F) = \{ X \to Y: X \to  Y \in F^{+} \wedge XY \subseteq R_{i} \}
$$

ovvero $F$ è l'unione di tutte le ...kszjhvskjhd

## Algoritmo


![[Recording 20241113155032.webm]]

Spiegazione passo passo del algoritmo:

![[Recording 20241113160006.webm]]


**Dimostrazione:**

![[Recording 20241113161258.webm]]

