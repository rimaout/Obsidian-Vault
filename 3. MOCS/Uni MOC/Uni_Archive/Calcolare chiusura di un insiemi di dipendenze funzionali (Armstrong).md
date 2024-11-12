---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2024-11-09T18:10
updated: 2024-11-09T21:26
---
>[!abstract] Related
>- 

---
## Introduzione 

è difficile calcolare F^* quindi l'idea è usare Armstrong per calcolare F^A (che è semplice) poi dimostriamo che F^+ = F^A

---
## Assiomi di Armstrong

Denotiamo con $F^{A}$ l’insieme di dipendenze funzionali
definito nel modo seguente:
- $\text{se}\ f \in F \text{ allora } f \in F^{A}$
- $\text{se}\ Y \subseteq X \subseteq R \text{ allora } X \to Y \in F^{A}$ [[#^f10628|(Assioma della Riflessività)]]
- $\text{se}\ X \to Y \in F^{A} \text{ allora } XZ \to  YZ \in F^{A}\ \ \ \ \forall Z \subseteq  R$ [[#^c39ea9|(Assioma dell'Aumento)]]
- $\text{se}\ X \to  Y \in F^{A} \text{ e } Y \to Z \in F^{A} \text{ allora } X \to  Z \in F^{A}$ [[#^b70ded|(Assioma della Transitività)]]

>[!danger] Assioma della Riflessività
>
>Se $Y \subseteq X \subseteq R$ allora $X\to Y \in F^{A}$
>
>>**Esempio:**
>>Supponiamo di avere un insieme di attributi $R = \{Indirizzo, Città, Provincia\}$ e un insieme di dipendenze funzionali $F^{A}$ definito come sopra.
>>
>>Se consideriamo l'insieme $X = \{Indirizzo, Città, Provincia\}$ e l'insieme $Y = \{Città\}$, possiamo vedere che $Y \subseteq X \subseteq R$.
>>
>>Secondo l'assioma della riflessività, questo significa che $X \to Y \in F^{A}$, ovvero $\{Indirizzo, Città, Provincia\} \to \{Città\} \in F^{A}$.
>>
>>Stessa cosa vale per $\{Indirizzo, Città, Provincia\} \to \{Indirizzo\}$ e $\{Indirizzo, Città, Provincia\} \to \{Provincia\}$ 

^f10628

>[!danger] Assioma dell'Aumento
>Se $X\to Y \in F^{A}$ allora $XZ \to YZ \in F^{A}$, per ogni $Z \in R$
>
>>**Esempio:**
>>Supponiamo di avere un insieme di attributi $R = \{Nome, Cognome, Età\}$ e un insieme di dipendenze funzionali $F^{A}$ definito come sopra.
>>
>>Se consideriamo l'insieme $X = \{Nome, Cognome\}$ e l'insieme $Y = \{Nome\}$, possiamo vedere che $X \to Y \in F^{A}$, ovvero $\{Nome, Cognome\} \to \{Nome\} \in F^{A}$.
>>
>>Secondo l'assioma dell'aumento, se aggiungiamo un nuovo attributo $Z = \{Età\}$ a $X$ e $Y$, allora la dipendenza funzionale $\{Nome, Cognome, Età\} \to \{Nome, Età\}$ è anche vera.

^c39ea9

>[!danger] Assioma della Transitività
>Se $X\to Y\in F^{A}$ e $Y \to Z \in F^{A}$ allora $X \to Z \in F^{A}$
>
>>**Esempio:**
>>Supponiamo di avere un insieme di attributi $R = \{Nome, Cognome, Indirizzo, Città\}$ e un insieme di dipendenze funzionali $F^{A}$ definito come sopra.
>>
>>Se consideriamo l'insieme $X = \{Nome, Cognome\}$ e l'insieme $Y = \{Indirizzo\}$, possiamo vedere che $X \to Y \in F^{A}$, ovvero $\{Nome, Cognome\} \to \{Indirizzo\} \in F^{A}$.
>>
>>Inoltre, se consideriamo l'insieme $Y = \{Indirizzo\}$ e l'insieme $Z = \{Città\}$, possiamo vedere che $Y \to Z \in F^{A}$, ovvero $\{Indirizzo\} \to \{Città\} \in F^{A}$.
>>
>>Secondo l'assioma della transitività, se $\{Nome, Cognome\} \to \{Indirizzo\}$ e $\{Indirizzo\} \to \{Città\}$, allora $\{Nome, Cognome\} \to \{Città\}$.

^b70ded

### Regole derivate dagli Assiomi

Altre tre regole che sono conseguenza degli assiomi di Armstrong che consentono di derivare da dipendenze funzionali in $F^{A}$ altre dipendenze funzionali in $F^{A}$.

>[!danger] Regola dell'Unione
>Se $X \to Y\in F^{A}$ e $X \to Z \in F^{A}$ allora $X \to YZ \in F^{A}$
>>[!warning]- Dim
>>Se $X \to Y \in F^{A}$ per assioma dell'aumento si ha $X \to XY\in F^{A}$.
>>- oss: $XX \to XY \equiv X \to XY$
>>
>>
>>Analogamente $X \to Z \in F^{A}$ diventa $XY \to YZ\in F^{A}$.
>>
>>Quindi per transitività abbiamo che $X \to YZ\in F^{A}$.

>[!danger] Regola della Decomposizione
> Se $X \to Y \in F^{A}$ e $Z \subseteq Y$ allora $X \to Z \in F^{A}$
> 
>>[!warning]- Dim
>>Se $Z\subseteq Y$ allora per riflessività si ha che $Y \to Z \in F^{A}$.
>>
>>Quindi poiché $X \to Y \in F^{A}$ e $Y \to Z \in F^{A}$ allora per transitività $X \to Z\in F^{A}$

>[!danger] Regola della Pseudo-Transitività 
>Se $X \to Y \in F^{A}$ e $WY \to Z \in F^{A}$ allora $WX \to Z \in F^{A}$
>
>>[!warning]- Dim
>>Se $X \to Y \in F^{A}$ per aumento si ha che $WX \to WY \in F^{A}$.
>>
>>Quindi dato che $WX \to WY\in F^{A}$ e $WY \to Z \in F^{A}$ allora per transitività abbiamo che $WX \to Z \in F^{A}$.

----