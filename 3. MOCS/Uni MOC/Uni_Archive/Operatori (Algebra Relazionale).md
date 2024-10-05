---
type: Uni Note
class:
  - "[[Basi di Dati 1 (class)]]"
academic year: 2023/2024
related:
  - "[[Algebra Relazionale]]"
completed: false
created: 2024-09-28T18:06
updated: 2024-10-05T15:14
---
>[!abstract] Index
>1. [[#Proiezione]]
>2. [[#Selezione]]
>3. [[#Unione]]
>4. [[#Differenza]]
>5. [[#Intersezione]]
>6. [[#Prodotto Cartesiano]]
>   
>   - [[Join-Naturale e Theta-Join (Algebra Relazionale)]]

>[!abstract] Related
>- [[Algebra Relazionale]]
>- [[Basi di Dati 1 (class)]]

---
## Proiezione

>[!note] Definizione
>La Proiezione consente di effettuare un “taglio verticale” su una relazione, cioè di selezionare solo alcune colonne (attributi).
>
>$$
>\pi_{A_{1}, A_{2}, \dots , A_{k}} (R)
>$$
>
>Dove:
>- $R$ è una relazione
>- $A_{1}, A_{2}, \dots , A_{k}$  sono gli attributi della relazione $R$ che vogliamo selezionare.

>[!example]- Esempio
>**Cliente**
>
>| Nome | C# | Città |
>| ---      | --- | ---    |
>| Rossi | C1 | Roma |
>| Rossi | C2 | Milano
>| Bianchi | C3 | Roma |
>| Verdi | C4 | Roma |
>
>>[!warning] Query
>>Nomi dei clienti, ovvero:
>>
>>$$
>>\pi_{\text{nome}}(\text{CLIENTE})
>>$$
>
>>[!todo] Output
>>
>>| Nome |
>>| --- |
>>| Rossi |
>>| Bianchi |
>>| Verdi |
>>
>>>**oss:** I doppioni vengono tagliati
>>>Se vogliamo conservare i clienti omonimi dobbiamo aggiungere un ulteriore attributo, in questo caso la «chiave» (il codice)

---
## Selezione

>[!note] Definizione
>LA Selezione consente di effettuare un "taglio orizzontale" su una relazione, cioè di selezionare solo le righe (tuple) che soddisfano una data condizione.
>
>$$
>\text{Selezione} = \sigma_{C}(r) 
>$$
>
>Dove: 
>- $C$ è una condizione (ovvero un espressione booleana composta da [[Operatori Booleani e Porte Logiche|operatori booleani]] e attributi con stesso dominio)
>- $r$ una relazione
>- $\text{Selezione}$ = le tuple di $r$ che soddisfano la condizione $C$

>[!example]- Esempio
>**Clienti**
>
>| Nome | C# | Città |
>| --- | --- | --- |
>| Rossi | C1 | Roma |
>| Rossi | C2 | Milano |
>| Rossi | C3 | Roma |
>| Bianchi | C4 | Roma |
>| Verdi | C5 | Roma |
>
>>[!warning] Query 1
>>Dati Dei Clienti che Risiedono a Roma:
>>
>>$$
>>\sigma_{\text{Citta } = \text{'Roma'}}(\text{Clienti})
>>$$
>>
>>**Output:**
>>
>>| Nome | C# | Città |
>>| --- | --- | --- |
>>| Rossi | C1 | Roma |
>>| Rossi | C3 | Roma |
>>| Bianchi | C4 | Roma |
>>| Verdi | C5 | Roma |
>
>>[!warning] Query 2
>>Dati dei clienti che si chiamano Rossi e risiedono a Roma:
>>
>>$$
>>\sigma_{\text{Citta } = \text{`Roma`} \wedge \text{Nome} = \text{`Rossi`}}(\text{Clienti})
>>$$
>>
>>**Output:**
>>
>>| Nome | C# | Città |
>>| --- | --- | --- |
>>| Rossi | C1 | Roma |
>>| Rossi | C3 | Roma |

---
## Unione

>[!note] Definizione
>L'unione costruisce una relazione che contiene tutte le ennuple appartengono ad almeno uno dei due operandi.
>
>$$
>r_{1} \cup r_{2}
>$$

>[!danger] Union Compatible
>L' operazione di unione può essere utilizzata soltanto su operandi **union compatible** cioè tali che:
>- hanno lo stesso numero di attributi.
>- gli attributi (nell'ordine) sono definiti sullo stesso dominio.
>
>>**oss:** non è necessario che gli attributi abbiano lo stesso nome, ma ovviamente il risultato ha senso se hanno un significato omogeneo.

^dd7bea

>[!example]- Esempio 1
>
>
>Supponiamo di avere due relazioni:
>
>>[!column|flex]
>>
>>>[!warning| clean no-icon] Relazione R
>>>
>>>| Nome | Età |
>>>| --- | --- |
>>>| Mario | 25 |
>>>| Luca | 30 |
>>>| Giovanni | 35 |
>>
>>>[!warning| clean no-icon] Relazione S
>>>
>>>| Nome | Età |
>>>| --- | --- |
>>>| Mario | 25 |
>>>| Luca | 30 |
>>>| Francesco | 20 |
>
>L'operazione di unione tra R e S, denotata come R ∪ S, restituisce una nuova relazione che contiene tutte le tuple presenti in R o in S.
>
>**R ∪ S**
>
>| Nome | Età |
>| --- | --- |
>| Mario | 25 |
>| Luca | 30 |
>| Giovanni | 35 |
>| Francesco | 20 |
>
>In questo esempio, la relazione R ∪ S contiene tutte le tuple presenti in R e S, senza duplicati. Le tuple (Mario, 25) e (Luca, 30) sono presenti in entrambe le relazioni, quindi sono incluse solo una volta nella relazione di unione.

>[!example]- Esempio 2 
>
>>[!column|flex]
>>
>>>[!warning|clean no-icon] Docenti
>>>
>>>| Nome | CodDoc | Dipartimento |
>>>| --- | --- | --- |
>>>| Rossi | D1 | Matematica |
>>>| Rossi | D2 | Lettere |
>>>| Bianchi | D3 | Matematica |
>>>| Verdi | D4 | Lingue |
>>
>>>[!warning| clean no-icon] Amministrativi
>>>
>>>| Nome | CodAmm | Mansioni |
>>>| --- | --- | --- |
>>>| Esposito | A1 | Contabilità |
>>>| Riccio | A2 | Didattica |
>>>| Pierro | A3 | Segreteria |
>>>| Bianchi | A4 | Didattica |
>
>>[!danger] Problema 
>>In questo caso non possiamo fare l'Unione tra `docenti` ed `amministrativi` perché anno dei domini diversi.
>
>>[!check] Soluzione 
>>Rimuoviamo l’attributo in più facendo una [[#Proiezione]]  su gli elementi comuni:
>>
>>$$
>>\text{Personale} = \pi_{Nome, CodDoc}(Docenti) \cup \pi_{Nome, CodAmm}(Amministrativi)
>>$$
>
>>[!column|flex]
>>
>>>[!warning|clean no-icon] Proiezione Docenti
>>>
>>>| Nome | CodDoc |
>>>| --- | --- |
>>>| Rossi | D1 |
>>>| Rossi | D2 |
>>>| Bianchi | D3 |
>>>| Verdi | D4 |
>>
>>>[!warning| clean no-icon] Proiezione Amministrativi
>>>
>>>| Nome | CodAmm |
>>>| --- | --- |
>>>| Esposito | A1 |
>>>| Riccio | A2 |
>>>| Pierro | A3 |
>>>| Bianchi | A4 |
>>
>>>[!warning| clean no-icon] Personale
>>>| Nome | CodAmm |
>>>| --- | --- |
>>>| Rossi | D1 |
>>>| Rossi | D2 |
>>>| Bianchi | D3 |
>>>| Verdi | D4 |
>>>| Esposito | A1 |
>>>| Riccio | A2 |
>>>| Pierro | A3 |
>>>| Bianchi | A4 |

---
## Differenza

>[!note] Definizione
>La differenza costruire una relazione contenente tutte le tuple che appartengono al primo operando e NON appartengono al secondo operando.
>
>$$
>r_{1} - r_{2}
>$$

>[!danger] Union Compatible
>Anche la gli operandi della differenza devono essere [[#^dd7bea|union compatible]].

>[!example]- Esempio
>
>Supponiamo di avere due relazioni:
>
>>[!column|flex]
>>
>>>[!warning| clean no-icon] Relazione R
>>>
>>>| Nome | Età |
>>>| --- | --- |
>>>| Mario | 25 |
>>>| Luca | 30 |
>>>| Giovanni | 35 |
>>
>>>[!warning| clean no-icon] Relazione S
>>>
>>>| Nome | Età |
>>>| --- | --- |
>>>| Mario | 25 |
>>>| Luca | 30 |
>>>| Francesco | 20 |
>
>L'operazione di differenza tra R e S, denotata come R - S, restituisce una nuova relazione che contiene solo le tuple presenti in R ma non in S.
>
>**R - S**
>
>| Nome | Età |
>| --- | --- |
>| Giovanni | 35 |
>
>In questo esempio, la relazione R - S contiene solo la tupla (Giovanni, 35) perché essa è presente in R ma non in S. Le tuple (Mario, 25) e (Luca, 30) sono presenti in entrambe le relazioni, quindi non sono incluse nella relazione di differenza.

---
## Intersezione

>[!note] Definizione
>L'intersezione costruisce una relazione contenente tutte le tuple che appartengono ad entrambi gli operandi.
>
>$$
>r_{1} \cap  r_{2}
>$$

>[!danger] Union Compatible
>Anche la gli operandi dell'intersezione devono essere [[#^dd7bea|union compatible]].

>[!warning] Correlazione con Differenza
>$$
>r_{1}\cap r_{2} = (r_{1} - (r_{1} - r_{2}))
>$$

>[!example]- Esempio 
>Supponiamo di avere queste due relazioni, e di voler creare una tabella che ci mostri il personale che è sia un docente e amministrativo, mostrando anche i ruoli.
>
>>[!column|flex]
>>
>>>[!warning|clean no-icon] Docenti
>>>
>>>| Nome | CodDoc | Dipartimento |
>>>| --- | --- | --- |
>>>| Rossi | D1 | Matematica |
>>>| Rossi | D2 | Lettere |
>>>| Bianchi | D3 | Matematica |
>>>| Verdi | D4 | Lingue |
>>
>>>[!warning| clean no-icon] Amministrativi
>>>
>>>| Nome | CodAmm | Mansioni |
>>>| --- | --- | --- |
>>>| Esposito | A1 | Contabilità |
>>>| Riccio | A2 | Didattica |
>>>| Piero | A3 | Segreteria |
>>>| Bianchi | A4 | Didattica |
>
>>[!check] Step 1 
>>Rinominare le colonne `CodDoc` e `CodAmm` (che anno significati analoghi) in modo da avere una colonna comune. Possiamo fare questo utilizzando l'operatore di rinominazione (ρ).
>>
>>$$
>>Docenti_rinominati = ρ_{Codice/CodDoc}​(Docenti)
>>$$
>>
>>>[!column|flex]
>>>
>>>>[!warning|clean no-icon] Docenti_Rinominati
>>>>
>>>>| Nome | Codice | Dipartimento |
>>>>| --- | --- | --- |
>>>>| Rossi | D1 | Matematica |
>>>>| Rossi | D2 | Lettere |
>>>>| Bianchi | D3 | Matematica |
>>>>| Verdi | D4 | Lingue |
>>>
>>>>[!warning| clean no-icon] Amministrativi_Rinominati
>>>>
>>>>| Nome | Codie | Mansioni |
>>>>| --- | --- | --- |
>>>>| Esposito | A1 | Contabilità |
>>>>| Riccio | A2 | Didattica |
>>>>| Pierro | A3 | Segreteria |
>>>>| Bianchi | A4 | Didattica |
>
>>[!check] Step 2
>> Ora possiamo effettuare l'intersezione tra le due relazione facendo attenzione ad escludere gli attributi `Dipartimento` e `Manzione` (non fanno parte dello stesso dominio) facendo una proiezione ($\pi$) su `Nome` e `Codice`.
>>
>>$$
>>\text{Intersezione} = \pi_{Nome, Codice}(Docenti\_rinominati) \cap \pi_{Nome, Codice}(Amministrativi\_rinominati)
>>$$
>>
>>| Nome | Codice |
>>| --- | --- |
>>| Bianchi | D3 |
>>| Bianchi | A4 |

---
## Prodotto Cartesiano

>[!note] Definizione 
>Il prodotto cartesiano costruisce una relazione che contiene tutte le possibili combinazioni di tuple dai due operandi.
>$$
>r_{1} \times r_{2}
>$$

>[!example] Esempio Base
>
>>[!column|flex] 
>>
>>>[!NOTE| clean no-icon] RelazioneA
>>>
>>>| Colore | Dimensione |
>>>| --- | --- |
>>>| Rosso | Grande |
>>>| Blu | Piccolo |
>>
>>
>>>[!NOTE| clean no-icon] RelazioneB
>>>
>>>| Forma | Materiale |
>>>| --- | --- |
>>>| Quadrato | Legno |
>>>| Cerchio | Metallo |
>
>>[!todo] Prodotto Cartesiano
>>
>>$$
>>\text{RelazioneA} \times \text{RelazioneB}
>>$$
>>
>>| Colore | Dimensione | Forma | Materiale |
>>| --- | --- | --- | --- |
>>| Rosso | Grande | Quadrato | Legno |
>>| Rosso | Grande | Cerchio | Metallo |
>>| Blu | Piccolo | Quadrato | Legno |
>>| Blu | Piccolo | Cerchio | Metallo |

>[!example] Esempio Con Complicazioni
>Abbiamo due Relazioni una che rappresenta i `clienti` l'altra che rappresenta gli `ordini` fatti dai clienti.
>
>In particolare ogni cliente ha un codice univoco `C#` che presente anche nell'ordine (sotto forma di `CC#`) per risalire al cliente che ha fatto l'ordine.
>
>>**Query:** Creare una tabella che mette in relazione i dati dei clienti e i dati degli ordini.
>
>>[!column|flex] 
>>
>>>[!NOTE| clean no-icon] Clienti
>>>
>>>| Nome | C# | Città |
>>>| --- | --- | --- |
>>>| Rossi | C1 | Roma |
>>>| Rossi | C2 | Milano |
>>>| Bianchi | C3 | Roma |
>>>| Verdi | C4 | Roma |
>> 
>>>[!NOTE| clean no-icon] Ordini
>>>
>>>| O# | CC# | A# | N-pezzi |
>>>| --- | --- | --- | --- |
>>>| O1 | C1 | A1 | 100 |
>>>| O2 | C2 | A2 | 200 |
>>>| O3 | C3 | A2 | 150 |
>>>| O4 | C4 | A3 | 200 |
>>>| O1 | C1 | A2 | 200 |
>>>| O1 | C1 | A3 | 100 |
>
>>[!todo] Prodotto Cartesiano
>>
>> $$
>>\text{Clienti} \times \text{Ordini}
>>$$
>>
>>| Nome | C# | Città | O# | CC# | A# | N-pezzi |
>>| --- | --- | --- | --- | --- | --- | --- |
>>| Rossi | C1 | Roma | O1 | C1 | A1 | 100 |
>>| Rossi | C1 | Roma | O2 | C2 | A2 | 200 |
>>| Rossi | C1 | Roma | O3 | C3 | A2 | 150 |
>>| Rossi | C1 | Roma | O4 | C4 | A3 | 200 |
>>| Rossi | C1 | Roma | O1 | C1 | A2 | 200 |
>>| Rossi | C2 | Milano | O1 | C1 | A1 | 100 |
>>| ... | ... | ... | ... | ... | ... | ... |
>>| Bianchi | C3 | Roma | O3 | C1 | A1 | 100 |
>>| ... | ... | ... | ... | ... | ... | ... |
>>| Verdi | C4 | Roma | O4 | A3 | 200 |
>>| ... | ... | ... | ... | ... | ... | ... |
>
>>[!danger] ERRORE
>>Come è possibile notare il codice cliente (`#C`) non combacia sempre con il codice cliente del ordine (`#CC`) per queste casistiche non è ottimale utilizzare il prodotto cartesiano, ma conviene utilizzar [[Join-Naturale e Theta-Join (Algebra Relazionale)|Join-Naturale o il Theta-Join]].


