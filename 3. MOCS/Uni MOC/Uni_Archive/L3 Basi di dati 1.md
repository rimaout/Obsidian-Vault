---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2024-10-02T15:30
updated: 2024-10-04T13:07
---
---
## Prodotto Cartesiano

^ba6198

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
![[Pasted image 20241003131140.png|500]]

(dove R1 ed R2 sono i nomi delle relazioni operando e A1,A2,..., Ak sono gli attributi comuni, cioè con lo stesso nome, delle relazioni operando) eliminando le ripetizioni degli attributi

$$
r_{1} \rhd  \lhd r_{2} = \pi(\sigma_{C}(r_{1} \times r_{2}))
$$

Dove:
- $C = R_{1} . A_{1} = R_{2} ∧ \dots ∧ R_{1}.A_{k} = R_{2}.A_{k}$
- $X$ è l'insieme di attributi $r_{1}$
- $Y$ è l'insieme di attributi di $r_{2}$ che non sono attributi di $r_{1}$

>[!danger] Da ricordare
>- nel join naturale gli attributi della condizione che consente di unire solo le ennuple giuste hanno lo stesso november
>- vengono unite le ennuple in cui questi attributi hanno lo stesso valore
>- Se non hanno stesso nome allora dobbiamo vedi appunti di mattia

>[!warning] oss
>- Quando i due operandi non hanno lo parametri comuni il join naturale si comporta come un [[#^ba6198|prodotto cartesiano]] .
>- $r_{1} \rhd  \lhd r_{2} = r_{2} \rhd  \lhd r_{1}$
>- $(r_{1} \rhd  \lhd r_{2})\rhd  \lhd r_{3} \neq r_{1} \rhd  \lhd (r_{2}\rhd  \lhd r_{3})$


>[!example]- Esempio
>![[Pasted image 20241002163928.png|600]]
>
>$$
>\text{Query:} \text{ Cliente } \rhd \lhd \text{ Ordine}
>$$
>
>**Risultato:**
>![[Pasted image 20241002170156.png|500]]

>[!example]- Esempio 2
>![[Pasted image 20241003133940.png|600]]


#### Casi Limite

>[!note] Caso limite 1
>Le relazioni contengono attributi con lo stesso nome ma non esistono ennuple con lo stesso valore per tali attributi in entrambe le relazioni
>- Risultato: il join naturale è vuoto
>  
>  >[!example]- Esempio
>  >![[Pasted image 20241003134955.png|400]]

>[!note] Caso limite 2
>![[Pasted image 20241003135137.png|600]]
>
>>[!example]- Esempio

#### Possibili Errori

- Ovviamente perché il join abbia senso gli attributi con lo stesso nome devono avere anche lo stesso significato

>[!example] Esempio
>![[Pasted image 20241003135420.png|400]]
>
>C# di artista non ha lo stesso significato di C# di Quadro, per avere senso, il join va effettuato tra Artista.C# e Quadro.Artista, quindi si usa un θ-join (vediamo dopo) oppure una ridenominazione.

---
## θ-join

Consente di selezionare le tuple del prodotto cartesiano dei due operandi che soddisfano una condizione del tipo:
$$
A \Theta B
$$

Dove:
- $\Theta$ è un operatore di confronto ($\Theta \in \{ <, =, >,\geq,\leq \}$)
- $A$ è un attributo dello schema del primo operando
- $B$ è un attributo dello schema del secondo operando
- $dom(A) = dom(B)$

