---
created: 2024-02-28T08:55
type: Uni Note
class: 
academic year: 2023/2024
related: 
completed: false
updated: 2024-05-27T13:29
---
---

>[!info] Index
>1. [[#Tipi primitivi]]
>2. [[#Variabili]]
>3. [[#Letterali (costanti)]]
>5. [[#Interi e virgola mobile]]

---

## Tipi primitivi
**Tipi di dati primitivi:**
- iNteri 
- Reali 
- Booleani
- Caratteri

>[!warning] oss:
>Stinge non sono tipi primitivi

**Aggiungi tabella operazioni appunti:**
![[Pasted image 20240228090958.png|500]]

>[!warning] oss:
>Se sommiamo/sottraiamo due caratteri in realtà stiamo sommando/sottraendo i numeri ascii associati a qui caratteri 

**Intervalli di rapresentazione:**
![[Pasted image 20240228091027.png|600]]

---
## Variabili 
Le variabili sono dichiarate esplicitando il tipo della variabile 
```
type variable
```

Questo tipo è detto statico, 

**Assegnazione:**
``` java
int contatore;
contatore = 0;
```

``` java
int contatore = 0;
```

>[!warning] oss
>Fanno stessa cosa

>[!def] Identificatori
Il nome che associamo alla variabile è detto identificatore, ovvero sequenza di lettere, cifre, _ e $ dove primo elemento della sequenza non può essere un numero
>- `case-sensitive` ("CIAO" diverso da "ciao")
>- non posso essere usate alcune parole riservate (es. public, static, int, double, ecc.)
>- Si utilizza la notazione [[Camel case]]

---
## Letterali (costanti)

>[!def] Definition:
>Un letterale una rappresentazione a livello di codice sorgente del valore di un tipo di dati
>- 27 o -32 sono letterali per gli interi
>- 3.14 è un letterale per i double
>- true o false sono gli unici due letterali per il tipo booleano
>- “Ciao, mondo” è un letterale per il tipo String

---
## Interi e virgola mobile
Le costanti di tipo **int** sono semplicemente numeri nell’intervallo [-2, +2] miliardi circa
- Costante di tipo long con vengono definite con il suffisso *l* o *L* (esempio 1000000000L) 

Le costanti di tipo **double** sono semplicemente numeri con la virgola (punto)
-  Le costanti di tipo float hanno il suffisso f o F (ad esempio,10.5f)


>[!tip]
>Trattino basso (\_) per separare le cifre 
>- es: 100_000 per indicare 100000
>
>Si può ottenere un intero da una rappresentazione binaria anteponendo 0b alla stringa binaria 
>- es: 0b101 vale 5

---
## Precedenza operatori aritmetici
![[Pasted image 20240228093922.png|600]]

---
## Caratteri
Un char è un carattere alfanumerico o un simbolo
- Ci sono $2^{16}$ (Codifica Unicode basata su interi a 16 bit) possibili valori di caratteri (più eventuali “caratteri supplementari”, per esempio per il cinese)
- **Definizione:** Racchiusi da apici (es. ‘a’, ‘b’, ‘0’, ‘1’, ecc.)

Caratteri di escape:
- Tab: `\t`
- A capo: `\n`
- Backslash: `\\`
- Apice: `\'
- Virgolette: `\''`

---
## Stringhe
 Una stringa è una sequenza di caratteri.

---
## Tipi Booleani

- Il tipo booleano ha solo due valori possibili: true (vero) e false (falso)
- Gli operatori disponibili sono && (and), || (or) e ! (not)

---
## Operatori confronto 

Risultato di un espressione che utilizza operatori di confronto ritornano come output una costante booleana

![[Pasted image 20240228094818.png|500]]




![[Pasted image 20240228095048.png|600]]

``` java
int a = 3;
int b = a++;
// a = 4
// b = 3

int z = (a++) - (c--) // expallin
```

``` java
int a = 3;
int b = ++a;
// a = 4
// b = 4

int z = (a++) - (c--) // explain
```

---
## Hello World
`filename: HellowWord.java`

```java
public class HelloWord
{
	public static void main(srting[] args)
	{
		System.out.print("Hello, Word!");
		System.out.println();
	}
}
```