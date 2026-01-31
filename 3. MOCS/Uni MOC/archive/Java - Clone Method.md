---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: true
created: 2025-01-28T17:43
updated: 2026-01-31T13:32
---
`clone()` è un metodo ogni classe eredita dalla super classe `object` e restituisce una copia dell’oggetto clonato (ovvero una nuova istanza dell'oggetto con stessi campi ma area di memoria diversa).

Normalmente non è possibile chiamare il metodo, per fare ciò dobbiamo l'interfaccia **segnaposto** `cloneable`, e poi effettuare un override e fornire un implementazione del metodo `clone()`.

>[!warning] Interfaccia Segnaposto
>
>L'interfaccia `cloneable` è detta interfaccia segna posto perché non contiene nessun metodo, infatti è semplicemente utilizzata per segnalare alla Java Virtual Machine che l’oggetto può essere clonato

### Clone Shallow Copy

Il metodo più semplice per effettuare un clone è semplicemente chiamare clone della super classe (object).

```java
public Object clone() {
	super.clone()
}	
```

Facendo ciò il risultato di `clone()` sarà una shallow copy ovvero, creeremo un nuovo oggetto con:
- I campi primitivi (ad esempio `int`, `boolean`, ecc.) saranno copiati e avranno valori identici all'oggetto originale.
- I riferimenti agli oggetti (ad esempio `String`, `Array`, ecc.) saranno copiati, ma punteranno alla stessa area di memoria dell'oggetto originale.

### Clone Deep Copy

Il metodo più complesso per effettuare un clone è creare però ogni campo che è riferimento ad un altro oggetto dovrà implementare `cloneable`  

Copia profonda dell'oggetto originale significa:
- I campi primitivi (ad esempio `int`, `boolean`, ecc.) saranno copiati e avranno valori identici all'oggetto originale.
- I riferimenti agli oggetti (ad esempio `String`, `Array`, ecc.) saranno copiati e creeranno nuove istanze degli oggetti riferiti, con valori identici all'oggetto originale.




