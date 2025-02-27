---
created: 2024-04-23T09:27
type: Uni Note
class: 
academic year: 2023/2024
related: 
completed: false
updated: 2025-02-27T10:15
---
---

>[!abstract] Index
>1. 

>[!abstract] Related
>- 

---
## for each sulle collection

- Le collection sono ora dotate di un metodo forEach che prende in input un’interfaccia Consumer\<? super T\> dove T è il tipo generico della collection
- Ad esempio:
- `Collection<String> c = Arrays.asList(ʺaaʺ, ʺbbʺ, ʺccʺ);`
- // In Java 7:
for (String s : c) System.out.println(s); // In Java 8:- c.forEach(s -> System.out.println(s)); // persino meglio:
c.forEach(System.out::println);

---
## Pila in java

- esempi di pila:
    
    - –  La pila di esecuzione (run-time stack) contenente i record di
        
        attivazione delle chiamate a metodi
        
    - –  Nell’implementazione della ricorsione...
        
- Esiste un’implementazione standard mediante la classe Stack
    
    – Implementa l’interfaccia List
    
- Operazioni principali:  
    – push: inserisce un elemento in cima alla pila  
    – pop: rimuove l’elemento in cima alla pila  
    – peek: restituisce l’elemento in cima alla pila senza rimuoverlo

---
### Come scegliere la migliore collezione 

![[Pasted image 20240423094241.png|800]]

---
## Gli alberi
- struttura basata su nodi con relazione padre figlio

>[!warning] Alberi più comuni sono binari

**Rappresentazione alberi in java:** 
```java
public class BinaryTree{
	private nodo root;

	static public class Nodo{
		private Nodo left;
		private Nodo right;
		private Nodo valore;
	}

	public Nodo(Nodo left, Nodo right, Nono Valore){
	a<dnl .hvkjgbcvh,zmr,jha b
	}
}
```

---
## Eccezioni
- Le eccezioni rappresentano un meccanismo utile a notificare e gestire gli errori
    
- Un’eccezione indica che durante l’esecuzione si è verificato un errore
    
- Il termine “eccezione” indica un comportamento anomalo, che si discosta dalla normale esecuzione
    
- Codice più robusto e sicuro

### Eccezioni notevoli

![[Pasted image 20240423100341.png|800]]

---
### Cosa si può gestire con le eccezioni

Errori sincroni, che si verificano a seguito dell’esecuzione di un’istruzione

- Errori non critici: errori che derivano da condizioni anomale • divisione per zero  
    • errore di I/O  
    • errori durante il parsing
    
-  Errori critici o irrecuperabili: errori interni alla JVM  
    • conversione di tipo non consentito  
    • accesso ad una variabile riferimento con valore null • mancanza di memoria libera  
    • riferimento a una classe inesistente

### Cosa non si può gestire
- Eventi asincroni
    
    - –  completamenti nel trasferimento I/O
        
    - –  ricezione messaggi su rete
        
    - –  click del mouse
        
- Eventi che accadono parallelamente all’esecuzione e quindi indipendenti dal flusso di controllo


---
### Try ... Catch


### `Throws` e `throw new`
**Throws:** utilizzato per indicare che 

**throw new**

### Finally
solitamente nel blocco `finally` vengono eseguite operazioni di clean up (es chiusura di file aperti ecc..)

### Politica catch or declare
- **Ignorare** l’eccezione e propagarla al metodo chiamante, a patto di aggiungere all’intestazione del metodo la clausola throws, seguìto dall’elenco delle eccezioni potenzialmente sollevate (declare)

- **Catturare** l’eccezione, ovvero gestire la situazione anomala in modo opportuno, prendendo provvedimenti e contromisure atte ad arginare il più possibile la situazione di emergenza (catch)

>[!warning]
>- Se il requisito catch-or-declare non viene soddisfatto il compilatore emette un errore che indica che l’eccezione dev’essere catturata o dichiarata

>[!danger]
>se main non ha throws allora siamo obbligati a gestire la possibile eccezione 
>se il main ha un throws allora possiamo anche non gestire l'eccezione e far terminare il programma ritornando l'eccezione sul terminale



---
## I metodi printStackTrace() e getMessage()


---
## Creare eccezioni personalizzate

```java
public class eccezioneX extends Exception{

}
```

---
## La classe Throwable

- La classe che implementa il concetto di eccezioni è Throwable che estende direttamente la classe Object
-  Gli oggetti di tipo Throwable sono gli unici oggetti che è possibile utilizzare con il meccanismo delle eccezioni

>[!info] Gerarchia delle eccezioni
>![[Pasted image 20240423110023.png|600]]

>[!info] Classe Exception
>- eccezioni interne alla JVM (classe RuntimeException): legate ad errori nella logica del programma
>- eccezioni regolari (es. IOException, ParseException, TimeoutException): errori che le applicazioni dovrebbero anticipare e dalle quali poter riprendersi
>
>**Checked exception:**
>-  È sempre necessario attenersi al paradigma catch-or-declar
>- Sono eccezioni comuni, ovvero quelle che estendono Exception (ma non RuntimeException)
>- Esempi:ParseException,ClassNotFoundException, FileNotFoundException
>
>**Unchecked exception:**
>- Non si è obbligati a dichiarare le eccezioni sollevate o a catturarle in un blocco try-catch (ma è possibile farlo)
>- Sono eccezioni che estendono Error o RuntimeException
>- Esempi: IndexOutOfBoundsException, ClassCastException, NullPointerException, ArithmeticException, OutOfMemoryError
    
>[!info] Classe Error
>- Error: cattura l’idea di condizione eccezionale irrecuperabile
>- Assai rari e non dovrebbero essere considerati dalle applicazioni (es. ThreadDeath, OutOfMemoryError...)

---