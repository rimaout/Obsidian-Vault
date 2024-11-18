---
created: 2023-03-22
type: Programming Note
programming language: "[[C MOC]]"
related:
  - "[[C Embedded  Functions]]"
  - "[[C malloc Function]]"
completed: true
updated: 2024-05-27T13:29
---
---
La funzione `free()` in C viene utilizzata per liberare la memoria allocata dinamicamente con la funzione `malloc()` (o altre funzioni di allocazione dinamica come `calloc()` o `realloc()`).

La funzione `free()` ha la seguente firma:
```c
void free(void* ptr);
```

**Input:**
- `ptr`: è un puntatore di tipo `void*` alla memoria da liberare.

>[!warning] 
> In realtà queta funzione non cancella i dati contenutti dalla memoria puntata dal puntatore ma semplicemente da il peresso al sistema operativo di modificarla

**Output:**
La funzione `free()` non restituisce alcun valore. Quando viene chiamata, la memoria puntata da `ptr` viene liberata e può essere utilizzata per altre allocazioni.

Ecco un esempio di utilizzo della funzione `malloc()` e `free()`:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int* arr = (int*) malloc(10 * sizeof(int));
    if (arr == NULL) {
        printf("Errore: memoria non disponibile\n");
        exit(1);
    }
    for (int i = 0; i < 10; i++) {
        arr[i] = i;
    }
    for (int i = 0; i < 10; i++) {
        printf("%d ", arr[i]);
    }
    free(arr);
    return 0;
}
```

- In questo esempio, viene allocato dinamicamente un array di 10 interi con la funzione `malloc()`. 
- Successivamente, l'array viene inizializzato con valori crescenti e stampato a schermo.
- Infine, la memoria allocata viene liberata con la funzione `free()`. 

---
## Non possibile liberare la memoria più volte 
E' importante notare che la chiamata a `free()` deve essere fatta solo una volta per ogni puntatore restituito da `malloc()`. 

Ecco un esempio di codice che tenta di liberare la stessa area di memoria più volte:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int* arr = (int*) malloc(10 * sizeof(int));
    if (arr == NULL) {
        printf("Errore: memoria non disponibile\n");
        exit(1);
    }
    for (int i = 0; i < 10; i++) {
        arr[i] = i;
    }
    free(arr);
    free(arr); // Tentativo di liberare la stessa area di memoria due volte
    return 0;
}
```

In questo esempio, viene allocato dinamicamente un array di 10 interi con la funzione `malloc()`. Successivamente, l'array viene inizializzato con valori crescenti. Tuttavia, viene tentato di liberare la stessa area di memoria due volte con la funzione `free()`. Questo può causare un errore di runtime o un comportamento indefinito del programma.

Pertanto, è importante assicurarsi di chiamare la funzione `free()` solo una volta per ogni puntatore restituito da `malloc()`.

## Non è possibile liberare una variabile locale 
Questo warning viene emesso dal compilatore quando si tenta di utilizzare la funzione `free()` su un puntatore che non è stato restituito da una funzione di allocazione dinamica come `malloc()`, `calloc()` o `realloc()`. 

La funzione `free()` viene utilizzata per liberare la memoria allocata dinamicamente, ovvero la memoria che è stata allocata durante l'esecuzione del programma con una funzione di allocazione dinamica. Questa memoria viene gestita dal sistema operativo e può essere liberata con la funzione `free()`.

D'altra parte, le variabili locali e i puntatori che puntano a variabili locali vengono allocate nello stack e vengono automaticamente liberate quando la funzione in cui sono dichiarate termina l'esecuzione. Queste variabili non devono essere liberate con la funzione `free()`, altrimenti si rischia di causare un comportamento indefinito del programma.

Ecco un esempio di codice che genera il warning "attempt to call free on non-heap object":
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int x = 10;
    free(&x); // Tentativo di liberare una variabile locale con la funzione free()
    return 0;
}
```

In questo esempio, viene dichiarata una variabile `x` di tipo `int` e viene tentato di liberarla con la funzione `free()`. Tuttavia, `x` è una variabile locale e non è stata allocata dinamicamente con una funzione di allocazione dinamica. Pertanto, la chiamata a `free()` genera il warning "attempt to call free on non-heap object".