---
type: Programming Note
programming language: "[[Java MOC]]"
related:
  - "[[Java Incapsulamento]]"
completed: true
created: 2024-06-16T18:49
updated: 2025-01-13T16:39
---
>[!abstract] Index
>1. [[#TLDR]]
>2. [[#Java Access Modifiers]]
>3. [[#Esempi]]

>[!abstract] Related
>- [[Java MOC]]
>- [[Java Incapsulamento]]

| Class     | Package | Subclass | World |     |
| --------- | ------- | -------- | ----- | --- |
| public    | Y       | Y        | Y     | Y   |
| protected | Y       | Y        | Y     | N   |
| default   | Y       | Y        | N     | N   |
| private   | Y       | N        | N     | N   |

---
## Java Access Modifiers

Gli access modifiers, o modificatori di accesso, sono parole chiave in Java che consentono di controllare il livello di visibilità e accessibilità degli elementi (classi, attributi e metodi) all'interno di un programma. 

>[!note] Private
>    - Gli elementi dichiarati come `private` sono accessibili solo all'interno della classe in cui sono definiti.
>    - Nessuna altra classe, nemmeno le sottoclassi, può accedere direttamente agli elementi `private`.
>    - Questo modificatore di accesso è il più restrittivo e garantisce il massimo livello di protezione dei dati.

>[!note] Protected
>    - Gli elementi dichiarati come `protected` sono accessibili all'interno della stessa classe, all'interno dello stesso package e nelle sottoclassi, anche se si trovano in un package diverso.
>    - Le sottoclassi possono accedere agli elementi `protected` della superclasse.
>    - Questo modificatore di accesso è utile quando si desidera consentire l'accesso alle sottoclassi, ma non all'esterno del package.

>[!note] Default
>    - Quando non si specifica alcun modificatore di accesso, Java utilizza il modificatore di accesso `default`.
>    - Gli elementi `default` sono accessibili all'interno dello stesso package, ma non sono accessibili da altri package.
>    - Questo modificatore di accesso offre un livello di protezione intermedio tra `private` e `public`.

>[!note] Public
>- Gli elementi dichiarati come `public` sono accessibili ovunque nel programma, sia all'interno che all'esterno della classe in cui sono definiti.
>- Nessuna restrizione di accesso viene applicata agli elementi `public`.
> - Questo modificatore di accesso offre il massimo livello di visibilità e accessibilità.

>L'utilizzo appropriato dei modificatori di accesso è fondamentale per l'[[Java Incapsulamento|incapsulamento]] e la modularità del codice Java. Essi consentono di nascondere i dettagli di implementazione e di esporre solo le informazioni necessarie all'esterno, promuovendo la riusabilità, la manutenibilità e la sicurezza del software.

---
## Esempi

>[!example] Public
>``` java
>class MyClass {     
>	private int x; // Accessibile solo all'interno della classe 
>}
>```

>[!example] Protected
>```java
>class SuperClass {
>	protected int z; // Accessibile all'interno della classe, del package e nelle sottoclassi 
>} 
>
>class SubClass extends SuperClass {     
>	// Può accedere a z 
>}
>```

>[!example] Default
>
>``` java
>package com.example; 
>
>class MyClass {     
>	int y; // Accessibile all'interno del package com.example 
>}
>```

>[!example] Public
>``` java
>public class MyClass {     
>	public int w; // Accessibile ovunque 
>}
>```