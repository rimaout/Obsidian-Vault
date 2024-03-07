Academic Year: 2022-2023
Class: [[Programmazione Calcolatori (Class)]]
Created: April 27, 2023
Tag: [[C MOC]]
Type: #Uni/Lecture 

---
# Multi Array (Matrici)

**Struttura:** un array che in modo immaginario viene suddiviso in righe e colonne (in realtà resta un singolo array consecutivo)

**Costo scrittura:** Costante (data una posizione il costo per scrivere in quella posizione è costante)

**Costo Lettura:** Costante (data una posizione il costo per leggere il valore associato a quella posizione è costante)

# Come calcolare posizione
- **Posizione array lineare:** riga * numero colonne * colonna
- **Coordinata colonna:** posizione_lineare %  numero_colonne
- **Coordinata riga:** posizione_lineare / numero_righe

# Funzioni 
**Funzione genera matrice:**
- Input: numero righe, numero colonne
- Output: matrice allocata dinamicamente

```c
float *crea_matrice(int nr, int nc) // nr = numero righe, nc = numero colonne
{
    float *mt = malloc(nr * nc * sizeof(float));     //allocazione memoria matrice

    int r, c; // r = righe, c = colonne

    if (mt == NULL){
        printf("Errore nell'allocazione della memoria");
        return NULL;
    }

    // Inizializzazione della matrice
    for (r = 0; r < nr; r++){
        for (c = 0; c < nc; c++){
            mt[r * nc + c] = r*c+1;
        }
    }
    return mt;
}
```

**Funzione stampa matrice per righe:**
- input: matrice, numero di righe e numero di collonne
- output: void (ma ne processo stampa la matrice per righe)

```c
void stampa_matrice(float *mt, int nr, int nc){ // mt = matrice, nr = numero righe, nc = numero colonne

    for (int r = 0; r < nr; r++){       // r = righe
        for (int c = 0; c < nc; c++){   // c = colonne
            printf("%f\t", mt[r * nc + c]);   // \t = tabulazione
        }
        printf("\n");   // \n = nuova riga
    } 
}
```


**Funzione stampa elemento in posizione p e le sue coordinate(riga, colonna):**
- Input: matrice, numero colonne della matrice e la posizione dell'elemento
- Output: coordinate dell'elemento e valore associato alla posizione
```c
void stampa_posizione(float *mt, int nc, int p){
// mt = matrice, nc = numero colonne matrice, p = posizione elemento
    int c = p % nc; // c = colonna
    int r = p / nc; // r = riga

    printf("M[%d, %d] = %f ", r, c, mt[p]);
}
```


# Matrice Array Array
**Struttura:** 
- Un array principale composto da puntatori agli  array righe (la lunghezza di questo array rappresenta il *numero di righe*)
- degli array (righe) sul quali vengono salvati gli elementi (la lunghezza massima di questi array rappresenta il *numero di colonne*)

![[IMG_6CB572C99D43-1.jpeg]]

**Costo scrittura:** Costante (data una posizione il costo per scrivere in quella posizione è costante)
**Costo Lettura:** Costante (data una posizione il costo per leggere il valore associato a quella posizione è costante)

**Vantaggi rispetto alla sruttura array base:** 
1. Occupa meno spazio in memoria (non siamo obbligati a creare righe che non ci servono, e le righe possono essere di simensioni diverse *oss:* dimensione massima resta uguale
2. Si adatta meglio a memorie frammentate (le righe possono essere scritte in memeoria in modo non consecutivo ma sparpagliato)

**Funzione genera matrice:**
- Input: numero righe, numero colonne
- Output: martice 

```c
float **crea_matrice(int nr, int nc){ // ** = puntatore a puntatore
	float **mt = malloc(sizeof(float*)*nr); // alloco array di puntatori
	
	if (mt == NULL){
		return NULL;
	}
	
	for(int r = 0; r < nr; r++){
		mt[r] = malloc(sizeof(float)*nc); // array di float (righe)
		
		if (mt[r] == NULL){ // se non riesco a allocare la riga
			
            // libero le righe già allocate
			for(int j = 0; j < r; j++){
				free(mt[j]);
			}

			free(mt); // libero l'array di puntatori
			return NULL;
		}
		
		for(int c = 0; c < nc; c++){ // inizializzo elemnti a 0
			mt[r][c] = 0;
		}
	}
	
	return mt;
}
```

**Funzione stampa matrice per righe:**
- input: matrice, numero di righe e numero di collonne
- output: void (ma ne processo stampa la matrice per righe)

```c
void stampa_matrice(float **mt, int nr, int nc){
		
	for(int r = 0; r < nr; r++){
		for(int c = 0; c < nc; c++){
			printf("%f\t ", mt[r][c] );
		}
		printf("\n");
	}
}
```