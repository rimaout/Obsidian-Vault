---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2024-12-12T13:21
updated: 2024-12-20T10:32
---
>[!abstract] Related
>- 

---
## Introduzione

Quando le chiavi ammettono un ordine, è più conveniente utilizzare un organizzazione fisica che tenga conto di questa caratteristica dei dati.

>[!note] Ordinamenti
>La maggior parte dei data type hanno un ordinamento
>- Valori numerici per confronto
>- Stringhe ordine lessicografico
>
>Se abbiamo dati composti da campi multipli, si ordina il primo campo, poi il secondo e cosi via (oss: l'ordinamento lessicografo si comporta allo stesso modo in cui i vari simboli rappresentano i campi)
>
>>[!warning]- Algoritmo di Ordinamento
>>
>>Le condizioni appena viste sono equivalenti al seguente algoritmo:
>>- Si pone n=1
>>- Si confrontano i simboli nella posizione n-esima della stringa:
>>    - Se una delle due non possiede l’elemento n-esimo allora è minore dell’altra e terminiamo
>>    - Se entrambe le stringhe non possiedono l’elemento n-esimo allora sono uguali e l’algoritmo termina
>>    - Se i simboli sono uguali si passa alla posizione successiva
>    - Se questi sono diversi, il loro ordine è l’ordine delle stringhe

## Inserimento

Quando inseriamo ma il blocchi sono piene, non possiamo effettuare operazioni per spostare (ri-organizzare) i blocchi in 
sadff


![[Pasted image 20241212135747.png|500]]

Blocco giallo in questo esempio è detto lista di overflow

## Indice denso

Supponiamo di definire più indice su lo stesso file. Ovvero creare un indice sulla chiave primaria e uno su una chiave secondaria.

Problema i due indici devono avere lo stesso ordine, 



## Esempio 1 

**oss:** in questo caso c'è scritto che ogni blocco deve essere pieno all 70%, in particolare qui quai è **al più** al 70% questo vuol dire che se calcoliamo la grandezza dei blocchi da utilizzare possiamo prendere la parte intera inferiore) al meno prendiamo la parte intera superiore.







