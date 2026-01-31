---
type: Uni Note
class:
  - "[[Basi di Dati 2 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-03-05T15:23
updated: 2026-01-31T13:32
---
## Introduzione

Risultano molto comuni, situazioni in cui diverse classi condividono gli stessi attributi. Il questo caso si può utilizzare il concetto di ereditarietà creando relazioni di sotto classi e super classi, proprio come in [[Java MOC|Java]] e nella [[[[Object Oriented Programming (OOP)|programmazione ad oggetti]] in generale. 

Tutti gli attributi, associazioni e le molteplicità della super-classe sono ereditati dalla sottoclasse.

## Costrutto is-a

Il costrutto is-a indica che una classe è sottoclassi di una solo altra classe, premettendo alla sotto classe di ereditare le caratteristiche della classe madre.

>[!example] Esempio
>
>![[Pasted image 20250306083500.png|400]]
>
>Ovviamente possiamo avere **relazioni is-a a più livelli**: **transitività**

Rispetto a [[Java MOC|Java]] l’ereditarietà in UML è molto più potente perché permette, infatti permette ad un oggetto di essere istanza di due classi, ad esempio:

![[Screenshot 2025-03-06 at 09.18.10.png|500]]

L’oggetto `Anna` è un istanza di `Studente`, ma anche di `Lavoratore`, a sua volta, essendo queste ultime sottoclassi di `Persona`, è anche implicitamente istanza di `Persona`. L’insieme delle sue classi più speci che è `{Studente, Lavoratore}`.

---
## Costrutto della Generalizzazione

 I diagrammi delle classi UML offrono un costrutto più complesso della relazione **is-a**, il costrutto della **generalizzazione**.
 
 Permette di definire che le istanze di una classe possono essere istanze di più classi figlie **secondo uno stesso criterio concettuale**.
 
 ![[Pasted image 20250306104904.png|1000]]

### Criteri {disjoint} e {complete}

Normalmente una istanza della classe base può essere istanza di più di una sottoclasse di una stessa generalizzazione.

Ad esempio in questo esempio una persona può essere: `Studente`, `Lavoratore`, `Studente e Lavoratore`, `ne Studente ne Lavoratore`.

![[Pasted image 20250306105938.png|500]]

É possibile porre delle limitazioni a questi comportamenti attraverso il [[#^44acd6|criterio {disjoint}]] ed il [[#^35dbf9|criterio {complete}]].

>[!note] Criterio {disjoint}
>
>![[Pasted image 20250306121455.png|450]]
>
>In questo caso la generalizzazione di `genere` è **disgiunta**, ovvero una istanza di `Uomo` non può essere anche istanza di `Donna`.
>
>Quindi una `Persona` o è un `Uomo` o è una `Donna`, o non è `ne Uomo ne una Donna`.

^44acd6

>[!note] Criterio {complete}
>
>![[Pasted image 20250306122944.png|450]]
>
>In questo caso la generalizzazione di `genere` è **completa**, ovvero ogni istanza di `Persona` deve essere anche istanza di almeno una sottoclasse tra `Uomo` e `Donna`.
>
>Quindi una persona o è un `Uomo` o è una `Donna`, o è `sia Uomo e Donna`.

^35dbf9

>[!note] Sia {disjoint} e {complete}
>
>![[Pasted image 20250306123414.png|400]]
>
>In questo caso la generalizzazione di `genere` è sia **completa** e **disgiunta**, ovvero ogni istanza di `Persona` deve essere anche istanza di esattamente una sottoclasse tra `Uomo` e `Donna`.
>
>Quindi una persona o è un `Uomo` o è una `Donna`.

## Ereditarietà Multipla

Una classe può essere sottoclasse di più classi. Il meccanismo dell’ereditarietà vale come sempre.

![[Pasted image 20250311180354.png|400]]

