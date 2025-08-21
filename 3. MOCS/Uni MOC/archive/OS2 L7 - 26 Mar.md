---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-03-26T09:08
updated: 2025-03-26T09:43
---
## Operatori

>[!note] Casting
>
>```c
>float z1 = 5.0/2;  // casting  implicito: output: 2.500000 
>float z2 = 5/2;    // casting  implicito: output: 2.000000
>float z3 = 5/2.0;  // casting  implicito: output: 2.500000
>float z4 = 5.0/2.0;  // casting  implicito: output: 2.500000
>float z5 = (float)5/2;  // casting  esplicito: output: 2.500000
>```

>[!note] Shorthand
>
>**Basi:**
>- `intVar++` corrisponde a `intVar = intVar+1`
>- `intVar--` corrisponde a `intVar = intVar-1`
>
>**Due opzion:** 
>- Post-incremento `x++`
>- Pre-incremento `++x`
>  
>**Esempio:**
>
>```c
>// Post Incremento
>n=2;
>r=2 * (n++);
>printf("r=%d, n=%d", r, n); //Output: r=4, n=3
>
>// Pre Inremento
>n=2;
>r=2 * (++n);
>printf("r=%d, n=%d", r, n); //Output: r=6, n=3
>```

## Loop

Esistono 3 tipologie di loop in C:

**while statement:** Più flessibile con nessuna tipo di restrizione

**for statement:** Ciclo ripetuto un numero intero di volte

**do-while statement:** Esegue il body almeno una volta