---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: true
created: 2025-02-05T18:55
updated: 2025-02-08T15:07
---
L'algoritmo per la cancellazione del tipo utilizzato dal *compilatore* per traduce il metodo/la classe generica in [[#^d36635|bytecode]] Java:
1. Elimina la sezione del tipo parametrico e sostituisce il tipo parametrico con quello reale
2. Per default il tipo generico viene sostituito con il tipo Object (a meno di vincoli sul tipo)
3. Viene creata una copia una copia della classe o metodo

Un generico equivale a un tipo Object su cui non devono essere fatte conversioni o downcasting. Non si posso conoscere il tipo generico a tempo di esecuzione per via della cancellazione del tipo.

>[!example] Esempio
>
>```java
>List`<Integer> x = new ArrayList<Integer>
>boolean b = x istanceof List`<Integer>
>```
>
>In questo caso il codice ritorna un eccezione perché non si posso conoscere il tipo generico a tempo di esecuzione per via della cancellazione del tipo (però da java 16 in poi funziona).

>[!note] Bytecode
>
>Quando si compila un programma Java, il compilatore Java traduce il codice sorgente Java in bytecode, che viene salvato in file con estensione `.class`. Il bytecode contiene le istruzioni che la JVM può eseguire per eseguire il programma.

^d36635
