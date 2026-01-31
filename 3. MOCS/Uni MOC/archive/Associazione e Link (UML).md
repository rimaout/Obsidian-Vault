---
type: Uni Note
class:
  - "[[Basi di Dati 2 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-02-27T10:49
updated: 2026-01-31T13:32
---
## Introduzione

Cosa sono le associazioni e i link:

- Un **ascoltazione** modella la *possibilità* che esista un legame tra oggetti di due (o più) classi.
- Un **link** è l'*istanza* di un associazione ovvero il legame effettivo tra due oggetti.

>***oss:*** un associazione può essere vista come un insieme di coppie ed un link come una coppia di quel insieme.

>[!warning] Livello intensionale ed Estensionale
>
> Le `associazioni` sono a livello *intensionale*. I `link` sono a livello *estensionale*

## Funzionamento

Ogni **associazione** e **link** sono rappresentati attraverso:
- un nome
- una linea che connette due classi/oggetti
- una freccia che indica la direzione di lettura (opzionale)

>***oss:*** i *link* non hanno un identificatore proprio, questo perché sono identificati dagli oggetti messi in relazione.

![[Pasted image 20250227111448.png|900]]

>[!note] Problema del Doppio Link
>
>Non è ammesso l'esistenza di due link della stessa associazione che uniscono gli stessi oggetti.
>
>![[Pasted image 20250227112026.png|850]]
>
>>***oss:*** per risolvere questo problema si possono sempre usare le [[#Classi Ponte]].

>[!note] Associazioni Multiple
>
>Tra le stesse classi possono essere definite più associazioni, che modellano legami di natura diversa.
>
>![[Pasted image 20250303213519.png|750]]

>[!note] Associazioni sulla stessa classe
>
>Quando una abbiamo un associazione che le lega la stessa classe dobbiamo definire i ruoli della associazione.
>
>![[Screenshot 2025-03-04 at 15.30.17.png|500]]
>
>- Ogni sovrano partecipa ad un numero di link con ruolo di successore che va da 0 a 1.
>- Ogni sovrano partecipa ad un numero di link con ruolo di predecessore cha va da 0 a 1.
>  
>  ![[Pasted image 20250304153344.png|700]]

## Classi Ponte

Se vogliamo creare un app che permette alla stessa persona di prenotare lo stesso hotel, non possiamo utilizzare questa rappresentazione:

>[!danger] Errore
>![[Pasted image 20250304093730.png|700]]
>
>>Schema preso dagli appunti di [@CasuFrost](https://github.com/CasuFrost/University_notes)

>[!done] Soluzione
>Per risolvere questo problema possiamo utilizzare una classe ponte, che fa tra intermediario tra hotel e persona:
>
 >![[Screenshot 2025-03-04 at 09.42.13.png|900]]

## Vincoli e Molteplicità

I vincoli di molteplicità sono utilizzati sulle *associazioni* per imporre delle restrizioni sul *numero di link* che possono esistere fra due classi.

![[Pasted image 20250303220136.png|1000]]

## Associazioni con Attributi

È possibile definire degli attributi che aggiungono informazioni alle associazioni. Per pare ciò si utilizzano le **association classes** delle classi che non rappresentano oggetti (infatti sono definite con lettere minuscole) ma associazioni.

![[Screenshot 2025-03-04 at 15.57.58.png|900]]

>[!warning] Problema del Doppio Link
>Continua a non essere ammessa l'esistenza di due link della stessa associazione che uniscono gli stessi oggetti, anche se questi due link hanno attributi diverso.
>
>>***oss:*** per risolvere questo problema si possono sempre usare le [[#Classi Ponte]].

>[!warning] Associazione con una Association Class
>
>Le association class possono par parte a loro volta di associazioni, ad esempio:
>
>![[Pasted image 20250304160104.png|800]]