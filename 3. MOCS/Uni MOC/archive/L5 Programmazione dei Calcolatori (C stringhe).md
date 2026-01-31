---
created: 2026-01-31T13:32
updated: 2026-01-31T13:32
---
Academic Year: 2022-2023
Class: [[Programmazione Calcolatori (Class)]]
Created: March 29, 2023
Tag: [[C MOC]]
Type: #Uni/Lecture 

---
# stinghe in c

sono array
```c
char a[] = "abcd"; 
```

## Carattere terminatore:
tutte le strighe contengono un carattere in più posizionato alla fine:
- es: contiene 4 caratteri + 1 terminatore (5 caratteri totali)
- carattere terminatore: '\\0' (null character)
- - è presente in tutte le stringhe

>[!warning]
>Quando creiamo una stringa in run time dobbiamo inserire noi il carattere terminatore

## Lunghezza stringa (non contano nullchar)
```c
#include <stdio.h>
// Function that returns the length of a string

int str_len(char *s){
	int i = 0;

	while(s[i] != '\0'){
		i++;
	}
	return i;
}
```

## Come funziona la stampa di una stringa
```c
int main(){
	char a[] = "Hello";
	int i = 0; // counter
	
	while(a[i] != '\0'){
		printf("%c", a[i]);
		i++;
	}
printf("\n");
```

## Concatenzione di stringhe V0
```c
char *str_cat0(char *s1, char *s2){ //versione 0 (non ottimizzata, infatti calcola 2 volte la lunghezza di s1 e s2)

	char *s3 = malloc(str_len(s1) + str_len(s2) + 1) * sizeof(char);
	int i = 0;

	for(i = 0; i < str_len(s1); i++){ // costo O(n^2)
		s3[i] = s1[i
	}
	for(i = 0; i < str_len(s2); i++){ // costo O(n^2) 
		s3[i] = s2[i-str_len(s1)];
	}

}
```
- Non è una funzione ottimizzata ogni volta ri calcola la lunghezza delle stringe
- Che inserita in un for ha un costo lineare

## Concatenzione di stringhe V1
```C
char *str_cat(char *s1, char *s2){ //versione ottimizzata
	char *s3 = malloc(str_len(s1) + str_len(s2) + 1) * sizeof(char);

	int i = 0;
	int n = str_len(s1); //costo O(n)
	int m = str_len(s2); //costo O(n)

	for(i = 0; i < n; i++){ // costo O(n)
		s3[i] = s1[i];
	}
	
	for(i = 0; i < m; i++){ // costo O(n)
	s3[i] = s2[i-n];
}
```
- Calcoliamo la lunghezza inizzialmente cosi da non dover ripetere il colacolo

# Strutture (struct)


## istruzione typedef
```c
typedef int intero
typedef struct array_int array_int
```
serve per cambiare nome a un istruzione 