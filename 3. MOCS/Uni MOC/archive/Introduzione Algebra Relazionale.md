---
type: Uni Note
class:
  - "[[Basi di Dati 1 (class)]]"
academic year: 2024/2025
related:
  - "[[Algebra Relazionale]]"
completed: true
created: 2024-10-09T16:36
updated: 2026-01-31T13:32
---
>[!abstract] Index
>1. 

>[!abstract] Related
>- [[Algebra Relazionale]]
>- [[Basi di Dati 1 (class)]]

---
## Relazione

>[!note] Definizione
>

Una relazione può essere rappresentata come una tabella in cui ogni riga è una tupla della relazione differente da ogni altra e ogni colonna è un attributo e corrisponde ad una componente (valori omogenei, cioè provenienti dallo stesso dominio).

>[!example] Example
>
>Relazione con due Tuple da 4 attributi:
>
>| Nome  | Cognome | Esami Sostenuti | Media |
>| ----- | ------- | --------------- | ----- |
>| Paolo | Rossi   | 2               | 26.5  |
>| Mario | Bianchi | 10              | 28,7  |

^80de85

>[!warning] Schema
>Lo schema di una relazione è la struttura logica di una tabella di una base di dati relazionale.
>
>Si rappresenta cosi $R(A_{1}, A_{2}, \dots, A_{k})$ dove $R$ è il nome della relazione e $A_{1}, A_{2}, \dots, A_{k}$ sono gli attributi.
>
>**Esempio:** $Studenti(\text{Nome},\ \text{Cognome},\ \text{Esami Sostenuti},\ \text{Media})$

^47e916

>[!warning] Istanza
>L’istanza di una relazione sono i suoi valore in un preciso instante nel tempo. [[#^80de85|Questo]] è un esempio di un istanza.

^2d7705

---
## Attributo

>[!note] Attributo
>Un attributo è definito da un **Nome** $A$ e dal **Dominio** dell'attributo $A$ che dichiamo con $dom(A)$

Gli attributi sono le colonne di una relazione, che rappresentano le proprietà o le caratteristiche dei dati. Gli attributi sono anche noti come campi o colonne.

>[!tip] Acesso
> Se t è un'ennupla su R ed A è un attributo in R, allora con t(A) indicheremo il valore assunto dalla funzione t in corrispondenza dell'attributo A.

---
## Dominio

Il dominio di un attributo è l'insieme di valori possibili che l'attributo può assumere. Ad esempio, se un attributo rappresenta l'età di una persona, il dominio potrebbe essere l'insieme di tutti i numeri interi positivi.

---
## Tupla

 Le tupla tuple sono gli elementi di una relazione a livello pratico una tupla è una singola riga di una relazione, che rappresenta un insieme di valori che soddisfano gli attributi della relazione. Una tupla è univocamente identificata dai suoi valori.

---
## Valori Nulli (null)

NULL è un valore valore polimorfo, ovvero non appartiene a nessun dominio ma può sostituire valori in qualsiasi dominio.

È utilizzato pre rappresentare mancanza di informazione, ovvero attributi di cui non conosciamo il valore.

>[!warning] Osservazione
>- Due valori NULL, anche se sullo stesso dominio, sono considerati diversi.
>- Le chiavi non devono mai avere valore NULL.

---
## Chiave

Una chiave di una relazione (non è detto che sia unica) è un attributo o insieme di attributi che identifica univocamente una tupla.

Una insieme di attributi $X$ per essere considerato una chiave di una relazione $R$ deve rispettare queste due condizioni:
1. Non devono esistere due tuple distinte $t_{1}$ e $t_{2}$ che hanno gli stessi valori per tutti gli attributi in $X$, tali cioè che $t_{1}[X] = t_{2}[X]$
2. Nessun sottoinsieme proprio di X soddisfa la condizione 1

>[!warning] Osservazioni
>- Una relazione potrebbe avere più chiavi, si sceglie come **chiave primaria** quella più usata o quella composta da un numero minore di attributi.
>- La chiave primaria non ammette valori nulli
>- Esiste sempre almeno una chiave (non possono esserci due tuple uguali)

---
## Vincoli di Integrità

I vincoli di integrità in algebra relazionale sono regole che definiscono le proprietà che i dati devono soddisfare per essere considerati validi e coerenti. 

Una [[#^2d7705|istanza]] di base di dati è corretta se soddisfa tutti i vincoli di integrità associati al suo [[#^47e916|schema]].