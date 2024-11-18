---
created: 2024-04-16T09:21
type: Uni Note
class: 
academic year: 2023/2024
related: 
completed: false
updated: 2024-05-27T13:29
---
---

>[!info] Page Index
>1. 

>[!info] Related Content
>- 

---
# Collezioni (collections)
• Le collezioni in Java sono rese disponibili mediante il
framework delle collezioni (Java Collection Framework)
• Strutture dati già pronte all’uso
– con interfacce e algoritmi per manipolarle
• Contengono e “strutturano” riferimenti ad altri oggetti
– Tipicamente tutti “dello stesso tipo”
• Alcune interfacce del framework:

## List
##### ArrayList

**Metodi**
- add
- get
- set
- remove

##### LinkedList
Stessi metodi + 
![[Pasted image 20240416093016.png|500]]

##### List Iterator



---
## Insiemi 
- Basati sull'interfaccia Set
- Elementi tutti distinti (no ripetizioni) oss: si usa equals per determinare l’uguaglianza
- Le classi insiemi `HashSet`, `TreeSet` e `LinkedHashSet` estendono `AbstarctSet` e implementano l'interfaccia `Set`

**HashSet**
- memorizza gli elementi in una tabella di hash
- oss: se stampo non si ha nessun ordinamento

**TreeSet:** 
- memorizza gli elementi in un albero (heap) mantenendo un ordine sugli elementi 
- oss: Se stampo ho un ordine dal più piccolo al più grande

**LinkedHashSet:** 
- memorizza gli elementi in ordine di inserimento
- oss: se stampo non si ha nessun ordinamento

---
## Mappe

• Una mappa mette in corrispondenza chiavi e valori
• Non può contenere chiavi duplicate
• java.util.Map è un’interfaccia implementata da HashMap, TreeMap e LinkedHashMap

**HashMap:** 
- memorizza le coppie in una tabella di hash

**TreeMap:** 
- memorizza le coppie in un albero mantenendo un ordine sulle chiavi

**LinkedHashMap:** 
- estende HashMap e mantiene l’ordinamento di iterazione secondo gli inserimenti effettuati

###### Metodi interfaccia Map

...

![[Pasted image 20240416100618.png|600]]

---
### java.util.Map

**Metodi**

forEach(BiConsumer)
– Itera su ciascuna coppia (chiave, valore)

getOrDefault(chiave, valoreDefault)
– Restituisce il valore associato alla chiave o valoreDefault se la
chiave non è presente

merge(chiave, valore, BiFunction)
– Se la chiave non contiene già un valore, imposta il valore
specificato, altrimenti chiama una bifunzione che decide come
mettere insieme il valore precedente con il valore passato in
input

of(chiave, valore, chiave, valore, ..., chiave, valore)
– statico, crea una mappa immutabile dei tipi e con i valori corrispondenti

---
### java.util.Collections

**Metodi**
![[Pasted image 20240416100837.png|500]]

---
### java.util.Arrays

**Metodi**
![[Pasted image 20240416100942.png|500]]

---
## Interfaccia Comparator
**Metodi di default:**
 -