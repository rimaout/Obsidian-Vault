---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2024-10-02T15:30
updated: 2024-10-02T17:04
---
>[!abstract] Index
>1. 

>[!abstract] Related
>- 

>[!danger] TLDR

---
## Unione

L'unione costruisce una relazione che contiene tutte le ennuple appartengono ad almeno uno dei due operandi.
$$
r_{1} \cup r_{2}
$$
>[!danger] Union Compatible
>L' operazione di unione può essere utilizzata soltanto su operandi **union compatible** cioè tali che:
>- hanno lo stesso numero di attributi.
>- gli attributi (nell'ordine) sono definiti sullo stesso dominio.
>
>>**oss:** non è necessario che gli attributi abbiano lo stesso nome, ma ovviamente il risultato ha senso se hanno un significato omogeneo.

^dd7bea

>[!example]- Example 
>![[Pasted image 20241002155110.png|500]]
>In questo caso non possiamo fare l'Unione tra `docenti` ed `amministrativi` perché anno dei domini diversi.
>
>**Soluzione:** Rimuoviamo l’attributo in più facendo una [[proiezione]]  su gli elementi comuni:
>
>$$
>\text{Personale} = \pi_{Nome, CodDoc}(Docenti) \cup \pi_{Nome, CodDoc}(Amministrativi)
>$$

---
## Differenza

La differenza costruire una relazione contenente tutte le tuple che appartengono al primo operando e NON appartengono al secondo operando.

$$
r_{1} - r_{2}
$$

>[!danger] Union Compatible
>Anche la gli operandi della differenza devono essere [[#^dd7bea|union compatible]].

---
## Intersezione

L'intersezione costruisce una relazione contenente tutte le tuple che appartengono ad entrambi gli operandi.

$$
r_{1} \cap  r_{2}
$$
>[!danger] Union Compatible
>Anche la gli operandi dell'intersezione devono essere [[#^dd7bea|union compatible]].

>[!warning] Correlazione con differenza
>$$
>r_{1}\cap r_{2} = (r_{1} - (r_{1} - r_{2}))
>$$

---
## Prodotto Cartesiano

Il prodotto cartesiano costruisce una relazione contenente tutte le ennuple che si ottengono concatenando una ennupla del primo operando con una ennupla del secondo operando.

$$
r_{1} \times r_{2}
$$

>[!warning] Utilizzo
>Si usa quando le informazioni che occorrono a rispondere ad una query si trovano in relazioni diverse

>[!example]- Esempio 1
>![[Pasted image 20241002163928.png|600]]
>
>>[!warning] Ridenominazione
>>Per poter distinguere gli attributi con lo stesso nome nello schema risultante possiamo usare l’operazione di ridenominazione (ρ)
>>$$
>>\text{OrdineR} = p_{cc \# } <- c \# (\text{ordine}) 
>>$$
>>
>>In questo caso rinominiamo `#c` di ordine in `#cc`.
>
>>[!warning] Prodotto cartesiano
>>$$
>>(\text{Cliente} \times \text{OrdineR})
>>$$
>>
>>![[Pasted image 20241002164939.png|600]]
>>
>>>Questo prodotto cartesiano in realtà non è corretto da un punto di vista pratico, visto che ad alcuni clienti sono ascoltati ordini fatti da altri clienti.
>>>
>>>**Vedi [[#^1232jnsjcks|Esempio 2]]** per una versione corretta.

**Da finireeeeee:**
>[!example]- Esempio 2


^1232jnsjcks

---
## Join Naturale

Il Join Naturale consente di selezionare le tuple del prodotto cartesiano dei due operandi che soddisfano la condizione:

$$
ckjnsjknkjnjkn
$$

(dove R1 ed R2 sono i nomi delle relazioni operando e A1,A2,..., Ak sono gli attributi comuni, cioè con lo stesso nome, delle relazioni operando) eliminando le ripetizioni degli attributi

>[!example]- Esempio
>![[Pasted image 20241002163928.png|600]]
>
>$$
>\text{Query:} \text{ Cliente } >< \text{ Ordine}
>$$
>
>**Risultato:**
>![[Pasted image 20241002170156.png|500]]

---