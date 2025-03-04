---
type: Uni Note
class:
  - "[[Basi di Dati 2 (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2025-02-27T10:49
updated: 2025-03-04T09:44
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

![[Pasted image 20250227111448.png|900]]

>[!note] Problema del Doppio Link
>
>Non è ammesso l'esistenza due link uguali (con stesso nome) che uniscono gli stessi oggetti.
>
>![[Pasted image 20250227112026.png|850]]
>

>[!note] Associazioni Multiple
>
>Tra le stesse classi possono essere definite più associazioni, che modellano legami di natura diversa
>
>![[Pasted image 20250303213519.png|750]]

## Vincoli e Molteplicità

I vincoli di molteplicità sono utilizzati sulle *associazioni* per imporre delle restrizioni sul *numero di link* che possono esistere fra due classi.

![[Pasted image 20250303220136.png|1000]]

## Classi Ponte

Se vogliamo creare un app che permette alla stessa persona di prenotare lo stesso hotel, non possiamo utilizzare questa rappresentazione:

![[Pasted image 20250304093730.png|700]]

>*errore* stesso link tra due classi tra le stesse due classi

Per risolvere questo problema possiamo utilizzare una classe ponte, che fa tra intermediario tra hotel e persona:

 ![[Screenshot 2025-03-04 at 09.42.13.png|900]]