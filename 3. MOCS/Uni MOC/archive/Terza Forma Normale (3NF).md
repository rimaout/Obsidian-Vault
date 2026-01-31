---
type: Uni Note
class:
  - "[[Basi di Dati 1 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2024-11-13T14:33
updated: 2026-01-31T13:32
---
---
## Introduzione

La terza forma normale è importante perché aiuta a ridurre la ridondanza dei dati e a migliorare la coerenza dei dati. Inoltre, essa facilita la gestione e la manutenzione dei dati, poiché riduce il numero di modifiche che devono essere apportate in caso di aggiornamenti o cancellazioni di dati.

>[!note] Definizione
>Dati uno schema di relazione $R$ e un insieme di dipendenze funzionali $F$ su $R$, 
>
>$R$ è in **3NF** se:
>$$
>\forall X \to  A \in F^{+} , A \not \in X
>$$
>
>Dove **almeno una** di queste due condizioni è verificata:
>- $A$ appartiene a una chiave (è primo)
>- $X$ contiene una chiave (è una super chiave)
>  
>>**oss:** È sbagliato scrivere $\forall X \to A\in F$ perché poi non sapremmo come valutare dipendenze del tipo $X\to AB$ ovvero con 2 o più attributi a destra, infatti in $F^{+}$  una dipendenza del tipo $X\to AB$ possiamo scomporla in $X\to A$ e $X\to B$.

>[!example]- Esempio 1
>$R = ABCD$
>$F = \{ AC\to B,\ B\to AD\}$
>
>Le chiavi sono $AC$ e $BC$
>
>**Valutiamo le dipendenze in $F$:**
>- $AC\to B$ va bene ($AC$ è una super-chiave)
>
>Ora non possiamo valutare $B \to AD$ perché il determinante $B$ non è super-chiave e per valutare il dipendente (parte destra) deve essere un singleton. Quindi dobbiamo dividere $B \to AD$ in $B \to A$ e $B \to D$ dipendenze che non sono in $F$ ma sono in $F^{+}$.
>
>**Valutiamo le dipendenze in $F^{+}$:**
>- $B \to A$ va bene ($A$ fa parte di una chiave quindi è detto primo)
>- $B \to D$ non rispetta la 3NF perché $B$ non è super-chiave e $D$ non è primo.
>  
>Quindi lo schema non è in 3NF.

>[!example]- Esempio 2
>$R = ABCD$
>$F = \{ AB \to CD,\ BC \to A, D \to AC \}$
>
>Abbiamo tre chiavi $AB$, $BC$ e $DB$.
>
>**Valutiamo le dipendenze in $F$:**
>- $AB\to CD$  va bene ($AB$ è super-chiave)
>- $BC \to A$ va bene ($BC$ è super-chiave e inoltre $A$ è primo)
>
>Ora non possiamo valutare $D \to AC$ perché il determinante $D$ non è super-chiave e per valutare il dipendente (parte destra) deve essere un singleton. Quindi dobbiamo dividere $D \to AC$ in $D \to A$ e $D \to C$ dipendenze che non sono in $F$ ma sono in $F^{+}$.
>
>**Valutiamo le dipendenze in $F^{+}$:**
>- $D \to A$ va bene ($A$ è primo)
>- $D \to C$ va bene ($C$ è primo)
>  
>  Quindi lo schema è in 3NF.

>[!warning] Nota importante
>
>Non è sufficiente considerare solo le dipendenze funzionali in $F$ , poiché non possiamo gestire le dipendenze con più attributi al dipendente (parte a destra). Invece, dobbiamo considerare le dipendenze funzionali in $F^{+}$, che includono anche le dipendenze derivate.

>[!note] Definizione Alternativa
>
>Siano R uno schema di relazione e F un insieme di dipendenze funzionali su R. Uno schema R è in 3NF **se e solo se** non esistono né [[#Dipendenze Parziali e Transitive|dipendenze parziali né transitive]] in `R`.
>
>>[!warning]- Dimostrazione di equivalenza con definizione originale
>>![[Pasted image 20241115162920.png|650]]
>>![[Pasted image 20241115162954.png|650]]
>>![[Pasted image 20241115163012.png|650]]

---
## Dipendenze Parziali e Transitive

>[!note] Dipendenze Parziali
>
>Siano $R$  uno schema di relazione e $F$  un insieme di dipendenze funzionali su $R$.
>
>$X \to  A \in F^{+}$ è una dipendenza parziale se:
>- $X$ è super chiave (contenuto in una chiave)
>- $A$ non è primo (non è contenuto da una chiave)
>  
>**Ovvero:** un attributo di una relazione dipende solo da una parte della chiave primaria.
> 
>>[!example]- Esempio
>>
>>$\text{Curriculum}(\text{Matr},\ \text{CF},\ \text{Cogn},\ \text{Nome},\ \text{DataN},\ \text{Com},\ \text{Prov},\ \text{C\#},\ \text{Tit},\ \text{Doc},\ \text{DataE},\ \text{Voto})$
>>
>>Dove:
>>- Le chiavi sono `Matr` e `C#`.
>>- Ad ogni numero di matricola (`Matr`) corrisponde un solo cognome (`Cogn`) 
>>
>>Quindi è possibile determinare la dipendenza `Matr C#` $\to$ `Cogn` e questa **dipendenza** è detta **parziale**.
>>
>>Per capirlo meglio abbiamo che l’attributo cognome `Cogn` **dipende parzialmente** dalla chiave `Matr C#` ovvero non serve la chiave intera per determinarlo ma soltanto una parte della chiave, infatti `Matr` è una parte dalla chiave e determina `Cogn`.

>[!note] Dipendenze Transitive
>
>Siano $R$ uno schema di relazione e $F$ un insieme di dipendenze funzionali su $R$.
>
>$X \to A \in F^{+}$ è una dipendenza transitiva su $R$ se:
>- $A$ non è primo
>- Per ogni chiave $K$ di $R$ abbiamo che $X$ non è contenuto propriamente in $K$ e $K-X \neq \emptyset$
>  
>**Ovvero:** un attributo di una relazione dipende transitivamente da un'altra parte della relazione che a sua volta dipende dalla chiave primaria.
> 
>>[!example]- Esempio
>>
>>$\text{Studente}(\text{Matr},\ \text{CF},\ \text{Cogn},\ \text{Nome},\ \text{Data},\ \text{Com},\ \text{Prov})$
>>
>>Dove:
>>- La chiave è `Matr` e `CF`.
>>- Ad un numero di matricola corrisponde un solo comune di nascita `Matr` $\to$ `Com`.
>>- Un comune si trova in una sola provincia `Com` $\to$ `Prov`.
>>
>>Quindi possiamo dire che `Matr` $\to$ `Prov` ovvero che ad una matricola corrisponde una sola provincia.
>>
>>In questo caso, la dipendenza transitiva è `Com` $\to$ `Prov`, poiché fa sì che l'attributo provincia dipenda transitivamente dalla chiave $\text{Matr}$ attraverso la dipendenza `Matr` $\to$ `Com` e `Com` $\to$ `Prov`.
>>
>>La dipendenza `Com` $\to$ `Prov` è detta dipendenza transitiva perché "causa" la transitività, ovvero fa sì che l'attributo provincia dipenda da un'altra parte della relazione che a sua volta dipende dalla chiave primaria.
