---
Created: 2024-02-29
Type: Uni Note
Class:
  - "[[Metodologie di Programmazione (class)]]"
Academic Year: 2023/2024
Related: 
Completed: false
---
---
## Arguments parsing 

```java
public class SommaInteri {
	public static voif(String[] args){
		int a = integer.parseInt(args[0]); // getting an int from the arguments
		int b = integer.parseInt(args[1]); // getting an int from the arguments

		System.out.print("La somma vale: ");
		System.out.println(a+b);
	}
}
```

## Somma di stinga + int
``` java
public class SommaInteri {
	public static voif(String[] args){
		String s = "La risposta alla domanda della vita, l'universo e tutto quanto è ";
		int v = 42;

		String risposta = s + v;
		System.out.println(risposta);
	}
}
```

## Casting 

**cast esplicito:**

**cast implicit:**


```java
// ESEMPI CASTING:

(int)2.71828               //output: 2 (int type)
Math.round(2.71828)        //output: 3 (long type)
(int) Math.round(2.71828)  //output: 3 (int type)
integer.perseInt("43")     //output: 42 (int type)
"42" + 99                  //output: "4299" (String type)
42 * 0.4                   //output: 16.8 (double type)
(int)42 * 0.4              //output: 16.8 (double type)
42 * (int)0.4              //output: 0 (double type)
(int)(42 * 0.4)            //output: 16.8 (double type)
```

>[!tip]
>Quando si effettua un casting implicito il risultato dell'operazione avrà lo stesso tipo del "operando più forte"
