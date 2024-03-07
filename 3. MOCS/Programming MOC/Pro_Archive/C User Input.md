---
Created: 2023-03-22
Type: Programming Note
Programming Language: "[[C MOC]]"
Related: 
Completed: true
---
---
## Index
1. [[#Interactive Input]]
2. [[#User input from the terminal]]

---
## Interactive Input
There are to function that interrupt the program and reed what the user is writing:
1. [[c scanf function]]  
2. [[c fgets function]]

---
## User input from the terminal 


**how to convert a user input string in other [[C Data Types|data types]]:**

```c

void main(int dim, char *args[]){
    // convertire lista di stringhr args in lista di interi
    int *a = malloc(sizeof(int)*(dim-2)); 
    //dim - 2 perchè il primo argomento è il nome del programma e il secondo è il numero di colonne
    int num;

    if(a == NULL){ //controllo se l'allocazione è andata a buon fine
        printf("Errore nell'allocazione di memoria");
        return;
    }
    
    for(int i=2; i<dim; i++){ //converto gli argomenti in interi
        if (sscanf(args[i], "%d", &num) == 1){ // se la conversione è andata a buon fine
            a[i-2] = num; //salvo il numero convertito nell'array
        } else {
            a[i-2] = 0; //se la conversione non è andata a buon fine, salvo 0 nell'array
        }
    }
```

Example input from terminal:
```terminal
gcc program.c

./a.out 1 3 5 7 9 11 13 15
```

```c
args = ["programma", "10", "1", "3", "5", "7", "9", "11", "13", "15"]
//oss: first 2 elements of args are the prgram name (programma) and the numbers of elements in args (10)

a = [1, 3, 5, 7, 9, 11, 13, 15]
//oss: the number of elements of a is the number of elemnts of args -2
```
