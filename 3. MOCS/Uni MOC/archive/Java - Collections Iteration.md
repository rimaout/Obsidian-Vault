---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: true
created: 2025-02-07T16:01
updated: 2025-02-07T17:16
---

È possibile **iterare esternamente** ad una collezione attraverso:
- l'oggetto [[Java - Notable Interfaces#Iterable e Iterator|iterator]] della collezione
- il costrutto *for each*
- indici se si utilizzano liste liste

È possibile **iterare internamente** ad una collezione attraverso attraverso:
- il metodo `forEach(Consumer<?> action)`
- funzioni degli [[Java - Streams]] come `forEach`, `map`, `filter`

>[!note] Iterator
>
>Per tutte le strutture dati che estendono `Collection` (e che quindi estendono `Iterable`) è possibile utilizzare l’oggetto iterator per iterare sulla collezione.
>
>```java
>ArrayList`<Persona> persone = new ArrayList<>();  
>persone.add(new Persona("Mario", "Rossi"));  
>persone.add(new Persona("Luca", "Bianchi"));  
>  
>Iterator`<Persona> iteratore = persone.iterator();  
>System.out.println(iteratore.next());   // print Mario Rossi  
>System.out.println(iteratore.next());   // print Luca Bianchi
>```
>
>>***Nota*** non è possibile utilizzare questo metodo su le mappe perché non estendono `iterable`.

>[!note] Costrutto For Each
>
>Il costrutto _for each_ in Java è un modo sintattico per iterare su una collezione, ma in realtà, il compilatore Java lo traduce in un ciclo _for_ tradizionale che utilizza un oggetto `Iterator` per iterare sulla collezione.
>
>```java
>for (Persona persona : persone) { 
>	System.out.println(persona); 
>}
>```
>
>Le mappe in Java non implementano l'interfaccia `Iterable` e quindi non è possibile utilizzare il costrutto *for each* direttamente su di esse.
>
>Tuttavia è possibile utilizzare il costrutto *for each* sul set delle chiavi della mappa (che si può ottenere con il metodo `keySet()`, che è un insieme di oggetti che implementa l'interfaccia `Iterable`. Poi passando le chiavi al metodo `get()` si possono ottenere i valori.
>
>```java
>// mappa: Matricola (Integer) -> Studente (Persona)
>Map<Integer, Persona> mappa = new HashMap<>(); 
>mappa.put("60237, new Persona("Mario", "Rossi"));
>mappa.put("75022", new Persona("Luca", "Bianchi"));
>
>for (Integer chiave : mappa.keySet()) {
>    Persona persona = mappa.get(chiave);
>    System.out.println(persona);
>}
>```

>[!note] Metodo forEach
>
>Tutte le collezione estendendo `Collection` che a sua volta estende `Iterable` ereditano il metodo `forEach`, metodo utilizzato per eseguire un'azione su ogni elemento di una collezione.
>
>```java
>`forEach(Consumer<?> action)`
>```
>
>Questo metodo prende in input un `Consumer`, ovvero un'interfaccia funzionale che contiene un metodo chiamato `accept(T ogg)`.
>
>Il metodo `accept()` dell'interfaccia `Consumer` viene chiamato per ogni elemento della collezione, passando l'elemento come input. In questo modo, è possibile eseguire un'azione personalizzata su ogni elemento della collezione.
>
>Essendo `Consumer` una classe funzionale ci sono diversi modi per implementarla, usando una [[Java - Lambda Function|lambda function]], una [[Java - Anonymous Classes|classe anonima]], un riferimento a metodo o implementandolo esplicitamente.
>
>```java
>persone.forEach(p -> System.out.println(p)
>```
>
>>[!example]- Modi per implementare Consumer
>>
>>In generale, le lambda expression e i riferimenti a metodo sono i modi più concisi e leggibili per implementare il `Consumer`, mentre le classi anonime e le implementazioni esplicite possono essere utili in situazioni più complesse
>>
>>**1. Implementazione esplicita:**
>>
>>```java
>>public class StampaConsumer implements Consumer`<String> {
>>    @Override
>>    public void accept(String s) {
>>        System.out.println(s);
>>    }
>>}
>>
>>List`<String> lista = Arrays.asList("a", "b", "c");
>>lista.forEach(new StampaConsumer());
>>```
>>
>>**2. Implementazione con lambda expression:**
>>
>>```java
>>List`<String> lista = Arrays.asList("a", "b", "c");
>>lista.forEach(s -> System.out.println(s));
>>```
>>
>>**3. Implementazione con riferimento a metodo:**
>>
>>```java
>>List`<String> lista = Arrays.asList("a", "b", "c");
>>lista.forEach(System.out::println);
>>```
>>**4. Implementazione con classe anonima:**
>>
>>```java
>>List`<String> lista = Arrays.asList("a", "b", "c");
>>lista.forEach(new Consumer`<String>() {
>>    @Override
>>    public void accept(String s) {
>>        System.out.println(s);
>>    }
>>});
>>```
>
>Anche se le Mappe non estendo `collection` o `Iterable` hanno comunque una loro implementazione di `forEach(BiConsumer<K, V>)` che utilizza un `BiConsumer` ovvero un consumer ma con due oggetti generici in input invece di 1.
