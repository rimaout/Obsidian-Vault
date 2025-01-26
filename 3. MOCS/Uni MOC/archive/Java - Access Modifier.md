---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: true
created: 2025-01-26T16:05
updated: 2025-01-26T16:06
---

---

>[!danger] TLDR
>
>|               | Class | Package | Subclass | World |
>| ------------- | ----- | ------- | ------------ | ----- |
>| **public**    | `Y`     | `Y`       | `Y`            | `Y`     |
>| **protected** | `Y`     | `Y`       | `Y`            | `N`     |
>| **default**   | `Y`     | `Y`       | `N`            | `N`     |
>| **private**   | `Y`     | `N`       | `N`            | `N`     |

Le keyword `public`, `private` e `protected` sono detti **access modifiers** (modificatori d’accesso) che consentono di controllare il livello di visibilità e accessibilità degli elementi (classi, attributi e metodi) all'interno di un programma. 

>[!note] Classi
>
>Normalmente le classi possono essere soltanto `Public` o con visibilità di `Default`:
>- Una classe `Public` è visibile in *tutto il progetto* indipendentemente dal package
>- Una classe con visibilità di `Default` (ovvero quando non scriviamo niente) indica che è visibile soltanto dalle altre classi che si trovano nello *stesso package*
>
>Le classi interne invece possono essere definite anche utilizzando anche i modificatori `Private` e `Protected`:
>- Una inner-class `Private` è visibile soltanto all'interno della classe in cui  definita
>- Una inner-class `Protected` è accessibile in tutto il *package* e in tutte le *sotto classi* della classe in cui è definita

>[!note] Campi e Metodi
>
>I campi e i metodi possono definiti con tutti e 4 i modificatori:
>- `Public` indica che il membro è visibile in qualsiasi classe e package del progetto
>- `Protected` indica che il membro è visibile in tutto il package e in tutte le sotto classi della calasse in cui è definito
>- `Default` (quando non si scrive niente) indica che il membro è visibile soltanto nel package della classe in cui è definito (e non nelle sotto classi)
>- `Private` indica che il membro è visibile soltanto nella classe in cui è definito

---
## Scopo

L'utilizzo appropriato dei modificatori di accesso è fondamentale per l'[[Java - Incapsulamento|incapsulamento]] e la modularità del codice Java. Essi consentono di nascondere i dettagli di implementazione e di esporre solo le informazioni necessarie all'esterno, promuovendo la riusabilità, la manutenibilità e la sicurezza del software.

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