---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2025-03-19T09:33
updated: 2026-01-31T13:32
---
[[C MOC]]

Struttura di una funzione:

```c
<return-type> fn-name (parameter-list)
	declaration of variables
	executable statements
```

>[!danger] Funzione main()
>
>Deve esistere una funzione main che verrà chiamata all'esecuzione del programma

>[!note] Return Statement
>
>Termina la funzione ritornando un valore, in C tutte le funzioni 

>[!note] Direttive
>
>Con il simbolo `#` stiamo dando delle direttive al precorressero, una direttiva molto comune è:
>
>```c
>#include <stdio.h>
>```
>- `stdio.h` file header che contiene costanti e prototipi funzioni
>- `< >` indicano che il file header e’ un file standard del C in `/usr/include`
>- `" "` indicano che il file header e’ dell’utente e si trova nella directory corrente o in un path specificato
>- `-I` permette di specificare le directory in cui cercare gli header file

>[!note] Commenti
>
>`// sono un commento` e `/* sono un commento */` indicano dei commenti.

## Compilazione e Precompilazione

>[!note] Precompilazione
>
>```
>cpp helloworld.c > precompilato.c
>```
>
>Il comando cpp server per pre-compilare un file c, l’output di questa operazione è un nuovo file c contenente le l'esecuzione delle direttive ed il codice presente nel file originale ma con i commenti rimossi.
>

 >[!note] Compilazione (di un precompilato)
 >
 >```
 >gcc -c precompilato.c -o helloword.o
>```
>- `-c` indichiamo che il file `precompilato.c`è già stato pre-compilato
>
>Funzionamento:
>- Controlla che la sintassi sia corretta
>- Controlla che venga rispettato il corrispettivo header (che quindi deve esistere al momento della chiamata!)
>- Crea effettivamente del codice macchina, ma solo per il contenuto delle funzioni. 
>- Ogni chiamata a funzione ha una destinazione simbolica.

>[!note] Compilazione
>
>```
>gcc -c file.c -o helloword.o
>```

>[!note] linking
>
>utilizzato sui file oggetto, ovvero i file che sono già stati convertiti in file macchina

## boo

>[!note] Argomenti da comandline
>
>```c
>main(int argc, char *args[]) 
>```
>
>- `argc` in dica il numero di argomenti
>- `args` è la lista contenente gli argomenti
>  
>>***oss:*** primo argomento è sempre il nome del eseguibile chiamato
>
>Ad esempio se creiamo il file `helloworld.c` definito in questo modo:
>
>```c
>#include <stdio.h>
>
>int main(int argc, char *args[]) {
>    printf("number of arguments: %d\n", argc);
>
>    printf("Arguments: %d\n", argc);
>    for (int i = 0; i < argc; i++) {
>        printf("args[%d] = %s\n", i, args[i]);
>    }
>}
>```
>
>Se lo compiliamo ed eseguiamo in questo modo:
>
>```shell
>gcc helloword.c -o eseguibile.o
>./eseguibile.o ciao sono una lista di argomenti
>```
>
>Otteniamo come output:
>
>```shell
>number of arguments: 7
>Arguments: 7
>args[0] = ./eseguibile.o
>args[1] = ciao
>args[2] = sono
>args[3] = una
>args[4] = lista
>args[5] = di
>args[6] = argomenti
>```

## Variabili 

Non possiamo utilizzare come nomi delle variabili le parole riservate come: `if, return, do, for, while, int, double, ...`.

Tre tipi di variabili:
- **Variabili Globali:** definite fuori delle funzione e sono accessibili in tutte le funzione
- **Parametri di Funzione:** nell’header di una funzione
- **Locali:** all’interno del blocco di codice di una funzione

Ci sono due modi per dichiarare le variabili locali di una funzione
- dichiararle all’inizio della funzione
- dichiarate nel punto più vicino al loro primo uso

>[!note] Dichiarate all’inizio della funzione
>
>Per motivi storici, nelle prime versioni di C si poteva dichiarare le variabili soltanto all'inizio della funzione, ancora oggi si utilizza dichiarare le variabili all'inizio di una funzione, quest💩o offre anche dei vantaggi:
>
>**Allocazione** - dichiarare tutte le variabili all’innizzio della funzione permette al compilatore di di allocare la memoria per tutte le variabili in una sola operazione, migliorando le performance e rendendo il memori layout pi semplice.
>
>**Visibilità** - è possibile vedere e 