---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: true
created: 2025-02-06T10:49
updated: 2025-02-06T15:14
---
## Introduzione

Il simbolo `?` è uno strumento che rendere i [[Java - Generic Types|tipi generici]] più flessibili. 

Può essere utilizzato al posto del nome di un tipo generico come **segnaposto**, in particolare si utilizza quando non è necessario conoscere il tipo parametrico da dare in input ad un oggetto di una classe con tipo generico.

```java
ArrayList<?> lista = new ArrayList<String>();
```

>[!warning] Limiti
>- **No tipo di ritorno:** non può essere utilizzato come tipo di ritorno di un metodo.
>- **No parametro di un costruttore:** non può essere utilizzato come tipo di parametro di un costruttore.

>[!example] Esempi Approfonditi
>
>**Utilizzo dell'operatore wildcard con una classe generica:**
>
>```java
>`ArrayList<?> lista = new ArrayList<String>();
>
>lista.add("Ciao"); // Errore di compilazione
>lista.toString();  // Si può fare  
>
>for (Object elemento : lista) { // Si può fare
>        System.out.println(elemento);
>}
>```
>
>**Utilizzo dell'operatore wildcard con un metodo**
>
>```java
>`public void stampaLista(List<?> lista) {
>	lista.add("Ciao"); // Errore di compilazione
>	lista.toString();  // Si può fare  
>    
>	for (Object elemento : lista) {
>        System.out.println(elemento);
>    }
>}
>```
>
>In questi esempi è possibile fare operazioni che non dipendono dal tipo della lista, ad esempio operazioni di lettura come to string, o un ciclo su gli elementi
>
>Non è possibile aggiungere un elemento alla lista, si ottiene un errore di compilazione, poiché il ***tipo di lista è sconosciuto*** e non si può garantire che l'elemento aggiuntivo sia del tipo corretto.
>
>È possibile risolvere questo problema limitando il tipo di dati che può essere utilizzato attraverso `extends`.

## Extends e Super

Il `? extends` e  `? super` sono un modi per limitare il tipo di dati che può essere utilizzato con l'operatore jolly `?` e sono utilizzati con la [[Java - PECS|convenzione PECS]].

Quando si utilizza `? extends`, si specifica che il tipo di dati deve essere una sotto-classe di un tipo specifico.

Quando si utilizza `? super`, si specifica che il tipo di dati deve essere una super-classe di un tipo specifico.

```java
List<? extends Number> a = new ArrayList<Number>();
List<? extends Number> b = new ArrayList<Integer>();
List<? extends Number> c = new ArrayList<Double>();
```

```java
List<? super Integer> x = new ArrayList<Number>();
List<? super Integer> y = new ArrayList<Integer>();
List<? super Integer> z = new ArrayList<Object>();
```

>[!example] Esempio Approfondito
>
>```java
>`List<? super Integer> lista = new ArrayList<Number>();
>lista.add(10); // Ok
>```
>
>In questo esempio, l'operatore jolly `?` è utilizzato con un limite superiore `super Integer`, il che significa che la lista può contenere solo elementi di tipo `Integer` o suoi supertipi. In questo caso, l'aggiunta di un elemento alla lista è consentita, poiché il tipo di lista è compatibile con il tipo dell'elemento aggiunto.

