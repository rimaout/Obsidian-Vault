---
type: Uni Note
class:
  - "[[Basi di Dati 2 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-02-27T10:30
updated: 2026-01-31T13:32
---
## Classi

Una classe modella un insieme di oggetti omogenei (le istanze della classe) ai quali sono associate *proprietà statiche* (attributi) e *dinamiche* (operazioni, le vedremo in seguito). 

Ogni classe e' descritta da:
- un nome 
- un insieme di proprietà (astrazioni delle proprietà comuni degli oggetti che sono istanze delle classi)

>[!note] Livello Intenzionale
>
>Le classi si dice che sono a livello **Intenzionale** .

>[!note] Rappresentazione
>
>![[Pasted image 20250227104319.png|600]]

---
## Oggetti

Un oggetto modella un elemento del dominio di analisi, questo oggetto è `autonomo`, ha un `identificatore univoco`, è istanza di una (o più) classi.

>***oss:*** quando un oggetto è istanza di più classi ne esiste sempre una più specifica

>[!note] Livello Estensione
>
>Gli oggetti sono a livello **estensione**.

>[!note] Rappresentazione 
>
>![[Pasted image 20250227104408.png|350]]
>
>In questo esempio:
>- ` div_comm` è l’*identificatore di oggetto* (scelto dall’analista per potersi riferire all’oggetto nello schema concettuale) 
>- `Libro` è la classe più specifica di cui l’oggetto è istanza
>
>>***oss:*** l’intestazione di un oggetto è sempre sottolineata.

## Esempio Classe ed Oggetti

![[Pasted image 20250227104754.png|1000]]

>[!note] Oggetti Duplicati
>
>Anche se concettualmente sbagliato nel linguaggio UML non è vietato definire due oggetti identici, a patto che differiscano per l’identificatore.

