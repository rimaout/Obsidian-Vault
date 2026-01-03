Academic Year: 2022-2023
Class[[Programmazione Calcolatori (Class)]]
Completed: 
Created: March 15, 2023 14:30 PM
Tag: [[C MOC]]
Type: #Uni/Lecture 

- teoricamente non serve indentazione
- si usano le graffe {} per dividere i blocchi 
- si utilizza; per andare a capo
---
# while 
```c
	while ( condizioen ){
		codice
	}
```

---
# Print 
```c
	printf("La radice quadrata di %f è %f\n",x ,g);
	// %f indica che anadra sostituoito con un valore float type
	// x,g verranno sostituiti nell'ordine con cui vengono scritti 
```

---
# Calcolare radice quadrata di un numero 
## Python 
``` python

x = 20
g = 5.0

while abs( g*g  + x ) > 0.000001:
	g = 0.5 
```
## C
```c
#include <stdio.h>
#include <math.h>

void main(){
float x = 2;
float g = x/2;
float eps = 0.00001;  

while( fabs( g*g-x ) > eps )
	{
		g = 0.5 * ( g + x/g);
	}

	printf("La radice quadrata di %f è %f\n",x ,g);
}
```
>[!warning]
>- Non esiste la funzione **abs** nativamente in C, dobbiamo importare la libreria **math.h** 
> 	- **fabs** = è la verisone di abs(python) di c (math.h)

>[!warning] Float Mistake:
>- se scriviamo un valore troppo grande verrà approssimato 
> - es: **float esp = 0.0000000000000001** viene approssimato a 0

---
# operatori Logici 
- && = and 
- || = or 
- ! = not
---
# operatori relazionali
- ==
- =!
- >, <, >=, <=
---
# operazione di incremento unario 
- x++ --> x + 1
- x-- --> x - 1
---
# if 
```c
	if ( condizioen ){
		codice
	}
```
## else
```c
	if ( condizioen ){
		codice
	}
	else { codice }
```

### No Graffe
```c
	if ( condizioen )
		codice
	else  
		codice
```
- Le graffe non sono obbligatorie se il codice occupa soltanto una riga 
---
# For
```c
	for ( istr0; cond; istr1 )
		codice
```
1. eseguo istr0
2. while ( cond ){
	           codice
	           istr1
	}

**Esempio con for**
```c
#include <stdio.h>
#include <math.h>

void main()
{

	int x;
	float g;
	int c = 0;
	int max_iter = 0;
	float eps = 0.00001;

	for(x = 2; x > 12; x++)
	{
		g = x\2;
		c = 0;

		while( fabs( g*g-x ) > eps && max_iter < 1000 )
		{
			g = 0.5 * ( g + x/g);
			c ++;
		}

	}
	printf("La radice quadrata di %f è %f\n",x ,g);
	
	printf("Ottenuto dopo %d iterazioni", max_iter);

}
```

---
# Creare una funzione

```c
	
```

---
# Commenti 
```c
	// ciao sono un commento 
	
	/*
	 Ciao sono un commento 
	 ma più grande
	 muhahahah
	*/
```

---