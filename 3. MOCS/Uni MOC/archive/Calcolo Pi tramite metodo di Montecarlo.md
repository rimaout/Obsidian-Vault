---
type: Uni Note
class:
  - "[[Programmazione Sistemi Multicore (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-11-06T17:27
updated: 2025-11-07T11:01
---
## Introduzione

Si vuole scrivere un programma che tramite il metodo di Montecarlo calcoli il valore stimato di $\pi$ distribuendo il lavoro su più processi tramite MPI. 

L’algoritmo utilizzato per il calcolo è semplice, si consideri un cerchio di *raggio unitario*, inscritto in un quadrato $2 \times 2$.

![[Pasted image 20251106173645.png|450]]

L’area del cerchio, è uguale a $πr^{2} \implies \pi$, l’area del quadrato è `4`. Sia $A_{c}$ l’insieme di tutti i punti compresi nel cerchio, e sia $A_{q}$ l’insieme di tutti i punti compresi nel quadrato. 

Risulta che il numero di punti nell’area del cerchio stanno all’area $\pi$, come il numero di punti che stanno nell’area del quadrato stanno a `4`.

$$
\frac{|A_{c}|}{\pi} = \frac{|A_{q}|}{4}
$$
In realtà, non ha senso considerare la cardinalità $|A_{c}|$ o di $|A_{a}|$, in quanto sono insiemi infiniti, supponiamo allora che tali insiemi siano finiti e di cardinalità `n`, si denotano $A^{n}_{c}$ e $A^{n}_{q}$, chiaramente $A^{n}_{c} \subseteq A^{n}_{q}$. Si ha che:
$$
\lim_{ n \to \infty } 4 \cdot  \frac{|A^{n}_{c}|}{|A^{n}_{q}|} = \pi
$$
L’algoritmo consiste nel :
- calcolare un numero `n` di punti casuali
- determinare il numero `c` di punti interni al cerchio, (ossia i punti `(x,y)` tali da rispettare $x^{2} + y^{2} \leq 1$)

Numericamente, $4 \frac{n}{c}$ approssimerà $\pi$, con una precisione sempre maggiore all’aumentare di `n`.

L’algoritmo si renderà parallelo, distribuendo equamente il numero di punti da calcolare a tutti i processi presenti.

## Codice

```c
#include "stdio.h"
#include "stdlib.h"
#include "time.h"
#include "mpi.h"
#include <stdio.h>

int main(int argc, char *argv[]) {
    int total_square_points = atoi(argv[1]); //più è alto maggiore è la precisione
    int total_circle_points;
    
    double x, y; //point coordinates
    int local_square_points, local_circle_points;
    int my_rank, comm_size;

    MPI_Init(NULL, NULL);
    MPI_Comm_rank(MPI_COMM_WORLD, &my_rank);
    MPI_Comm_size(MPI_COMM_WORLD, &comm_size);
        
    srand(time(NULL));
     
    local_square_points = total_square_points / comm_size;
    for (int i=0; i<local_square_points; i++) {
        //point generation
        x = 2 * (rand() / (double)RAND_MAX) - 1;
        y = 2 * (rand() / (double)RAND_MAX) - 1;
        
        if (x*x + y*y <= 1 ) { // controllo se il punto è nel cerchio
            local_circle_points++;
        }
    }

    MPI_Reduce(&local_circle_points, &total_circle_points, 1, MPI_INT, MPI_SUM, 0, MPI_COMM_WORLD);

    if (my_rank == 0) {
        double pi_estimate = (double)total_circle_points / (double)total_square_points * 4; 
        printf("Estimate of pi = %f\n", pi_estimate);
    }

    MPI_Finalize();
    return 0;
}
```
