---
type: Programming Note
programming language: General
related:
  - "[[Software Design Pattern]]"
  - "[[Metodologie di Programmazione (class)]]"
completed: true
created: 2024-06-16T16:49
updated: 2025-05-10T13:36
---
>[!abstract] Related
>- [[Software Design Pattern]]
>- [[Metodologie di Programmazione (class)]]

---
## Introduzione 

>**Per vedere la spiegazione completa di questo design patter vedi: [Refactoring Guru - Singleton Design Pattern](https://refactoring.guru/design-patterns/singleton)**

>[!note] Idea di base
>**Obbiettivo:** 
>- Assicurarsi che una determinata possa avere una sola istanza, e allo stesso momento deve avere un punto di accesso globale.
>
>**Soluzione:** 
>- Rendere privato il costruttore predefinito, per evitare che altri oggetti utilizzino l'operatore new
>- Creare un metodo di creazione statico che funga da costruttore. Questo metodo richiama il costruttore privato per creare un oggetto e lo salva in un campo statico. Tutte le chiamate successive a questo metodo restituiscono l'oggetto memorizzato nella cache.

>[!example] Esempio
>``` java
>public class Ferrovie{
>	private static Ferrovie instance;
>	private ArrayList<Corsa> corse;
>
>	private Ferrovie(){ 
>		corse = new ArrayList<Corsa>();
>	}
>
>	public static Ferrovie getInstance() { 
>		if (instance == null) {
>			instance = new Ferrovie();
>		}
>	return instance;
>	}
>}
>```

