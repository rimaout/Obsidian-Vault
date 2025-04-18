---
type: Programming Note
programming language: 
related: 
completed: false
created: 2025-04-17T14:42
updated: 2025-04-18T18:51
---
## Introduzione (Memoria e Puntatori)

La memoria è organizzata in celle di dimensione fissa (tipicamente 8 bit, cioè 1 byte). Ogni cella ha un indirizzo unico.

>[!note] Dimensione Variabili
>
>Ogni variabile occupa un certo numero di celle consecutive:
>- Un `char` occupa 1 cella.
>- Un `int` tipicamente occupa 4 celle (4 byte).
>  
>>[!question]- Pesi dei datatypes
>>
>>|Type|Size (bytes)|
>>|---|---|
>>|`int`|at least 2, usually 4|
>>|`char`|1|
>>|`float`|4|
>>|`double`|8|
>>|`short int`|2 usually|
>>|`unsigned int`|at least 2, usually 4|
>>|`long int`|at least 4, usually 8|
>>|`long long int`|at least 8|
>>|`unsigned long int`|at least 4|
>>|`unsigned long long int`|at least 8|
>>|`signed char`|1|
>>|`unsigned char`|1|
>>|`long double`|at least 10, usually 12 or 16|

>[!note] Dimensione Puntatori
>
>La dimensione di un puntatore dipende dall’architettura del sistema:
>- Su sistemi a 32 bit: 4 celle (4 byte).
>- Su sistemi a 64 bit: 8 celle (8 byte).
>
>Lo spazio occupato da un puntatore non dipende dal tipo che punta, infatti un puntatore rappresenta un indirizzo di memoria in cui è presente l'elemento che stiamo puntando, quindi:
>
>```c
>printf("char: %lu byte - int: %lu byte\n", sizeof(char), sizeof(int));
>printf("char pointer: %lu byte - int pointer: %lu byte\n", sizeof(char*), sizeof(int*));
>
>//Output:
>//  char: 1 byte - int: 4 byte
>//  char: 8 byte - int: 8 byte
>```

## Sintassi Puntatori (C)

La sintassi dei puntatori è composta da due simboli speciali `*` e `&`, dove in particolare `*` in base al contesto assume significati diversi.

>[!note] Dichiarazione
>
>Possiamo utilizzare la sintassi `datatype *var_name` per dichiarare un puntatore.
>
>```c
>char *pc;
>```
>
>In questo caso stiamo dicendo che `pc` è un puntatore ad un area di memoria di 1 byte (grandezza di un char).
>
>Più a basso livello la variabile `p` contiene l'indirizzo della cella di memoria che sta puntando.

>[!note] Dereferenziazione (modifica/lettura)
>
>Possiamo utilizzare l'operatore di dereferenziazione `*` per accedere all'indirizzo di memoria puntato dal puntatore e leggere/modificare il valore contenuto.
>
>```c
>*pc = 'c';           // lettura
>printf("%c", *pc);   // modifica
>```

>[!note] Indirizzo
>
>In `C` è possibile accedere all'indirizzo di una variabile attraverso l'operatore `&`, possiamo utilizzare questo operatore per puntare variabili già esistente.
>
>```c
>char c = 'x'
>pc = &c
>```
>
>Scriviamo `pc = &c` e non `pc* = &c` perché:
>
>| Sintassi    | Significato                                         | Corretto? |
>| ----------- | --------------------------------------------------- | --------- |
>| `pc = &c;`  | Assegna a `pc` l'indirizzo di `c`                   | ✔️        |
>| `*pc = c;`  | Assegna al valore puntato da `pc` il valore di `c`  | ✔️        |
>| `*pc = &c;` | Assegna al valore puntato da `pc` l' indirizzo di `c`  | ❌         |
>| `pc = c;`   | Assegna a `pc` (che dovrebbe contenere un indirizzo) il valore di `c` (ovvero `'x'`)| ❌         |

>[!tip] 
>
>```c
>int *px = &x;
>int y = *px
>```
>Possiamo leggere:
>- `int *px = &x` --> il puntatore ad intero `px` contiene l’indirizzo della variabile `x`.
>- `int y = *px` --> la variabile intera `y` contiene il valore contenuto dalla indirizzo di memoria puntato da `px`.
