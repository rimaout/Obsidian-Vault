---
created: 2023-06-26
type: Uni Note
class:
  - "[[Metodi matematici per l'informatica (class)]]"
related:
  - "[[Dimostrazione diretta]]"
  - "[[Dimostrazione per assurdo]]"
  - "[[Dimostrazione per induzione]]"
  - "[[Dimostrazione contro nominale]]"
  - "[[Dimostrazione per contro-esempio]]"
completed: 
updated: 2024-05-27T13:29
---
---
# Indice
1. [[#Definizione]]
2. [[#Metodi Dimostrativi]]
	1. [[#Dimostrazione diretta]]
	2. [[#Dimostrazione per assurdo]]
	3. [[#Dimostrazione contro nominale]]
	4. [[#Dimostrazione per contro-esempio]]
	5. [[#Dimostrazione per induzione]]
	
---
# Definizione 
Una **dimostrazione matematica** è un *processo deduttivo* che permette di *verificare la validità dell'enunciato di un teorema*, e che prevede di mostrare che la validità delle **ipotesi** implica la validità della **tesi**

$$ Ipotesi \implies Tesi $$

>[!warning] Oss:
>In un impianto dimostrativo le ipotesi sono tutte le condizioni o proprietà che si suppongono vere, e vengono solitamente introdotte mediante la congiunzione condizionale se; al contrario, la tesi è la condizione o proprietà che discende dalle ipotesi, e viene solitamente introdotta dalla congiunzione coordinativa allora.

---
# Metodi Dimostrativi

É possibile dimostrare un ipotesi attraverso diversi metodi dimostrativi:

### [[Dimostrazione diretta]]: 
- Ragionamento deduttivo in cui, supponendo vere le ipotesi, permette di giungere alla tesi anche grazie a postulati, assiomi o principi di partenza o eventualmente a proposizioni, teoremi, lemmi o corollari precedentemente dimostrati.

### [[Dimostrazione per assurdo]]:
- Si suppongono le ipotesi vere e si suppone che la tesi non sia valida; si innesca un ragionamento che conduce a una contraddizione con le ipotesi.

### [[Dimostrazione contro nominale]]:
- detta anche dimostrazione per contrapposizione, prevede di dimostrare che la negazione della tesi implica la negazione dell'ipotesi.

### [[Dimostrazione per contro-esempio]]:
- metodo usato per dimostrare che un enunciato è falso, prevede di individuare un esempio che soddisfa le ipotesi e che contraddice la tesi.

### [[Dimostrazione per induzione]]:
- si utilizza per dimostrare un teorema o una proprietà in cui l'asserto è espresso mediante numeri naturali o è comunque tale da presentare una dipendenza dai numeri naturali, tipicamente riconducibile alla forma:
	1. *Passo iniziale:* verificare che sia vera la proprietà P(0);
	2. *Passo induttivo:* supporre che sia vera la proprietà P(m) (detta ipotesi induttiva) e dimostrare che da ciò segue la validità della proprietà P(n + 1).

Ultimata la verifica dei punti 1) e 2) la dimostrazione per induzione è completa e si può asserire che la proprietà P(n) è vera per ogni n E N.

---