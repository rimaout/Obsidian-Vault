---
type: Uni Note
class: "[[Basi di Dati 2 (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2025-06-18T12:50
updated: 2025-06-18T15:58
---
## Introduzione

Documento separato da accludere allo schema concettuale in cui vengono specificate:
- La descrizione della classe
- Specifica delle operazioni

![[Pasted image 20250319154245.png|1000]]

## Descrizione della classe

La descrizione della classe è una breve descrizione della classe 🤦.

## Specifica delle Operazioni

Per ogni classe dobbiamo effettuare la specifica di tutte le operazioni che ne appartengono.

La specifica di un operazione segue il seguente template:

```
nome operazione(parametri) : tipo ritorno
	
	pre condizioni
	...
	...
	...

	post condizioni
	...
	...
	...
```

>[!note] Pre-condizioni
>
>Sono le condizioni che devono essere soddisfatte dalle istanze per far si che l’operazione possa essere invocata, definiscono il cosiddetto *contratto dell’operazione*.
>
>Specificano anche se l’operazione modifica o no il livello degli oggetti.
>
>Queste condizioni possono riguardare:
>- campi o stai dell'oggetto (this) di invocazione
>- valori dei parametri in input
>- altri oggetti del sistema

>[!note] Post-Condizioni
>
>Le post condizioni danno la definizione matematica dell’operazione e del valore che restituisce.
>
>Deve essere segnalato e l’operazione modifica o no il livello degli oggetti (le istanze presenti).
>
>- Definiscono il tipo di ritorno
>- Definizione delle modifiche all’insieme degli oggetti esistenti, creazione di nuovi oggetti o link, eliminazione di oggetti o link
