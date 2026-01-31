---
created: 2023-04-26T19:54
updated: 2026-01-31T13:32
---
Academic Year: 2022-2023
Class: [[Programmazione Calcolatori (Class)]]
Created: March 12, 2023
Tag: [[C MOC]], [[Python Dictionaries in C]], [[Python Dictionaries]]
Type: #Uni/Lecture 

---

# Ricreare dizionari di python in c
**def:** insiemi di coppie di chiavi e di valori

**Operazioni da svolgere:**
- creare nuovo dizionario (vuoto)
- inserire nuovi elementi (chiavi + valore) --> *set*
- Modifica di un valore associato ad una coppia
- Cancellazione di un elemento (input chiave)
- Lettura (input chive, output: valore)
- Ricerca( input chiave, output True o False)

**oss:** In [[Python MOC]] tutte tutte le operazioni sui dizionari hanno costo costante tranne la ricerca che ha costo lineare

***?perché  medio e non nel caso peggiore***

---

# Implementazione
Possiamo utilizzare sia un array (normale),  o una lista concatenata 

***in entrambi i casi non sarebbe possibile avere costo costante per la maggior parte delle operazioni***

**Esempio utilizzando lista concatenata:**
![[IMG_499D7F381877-1 1.jpeg]]


## Implementazione stile python

#### **Strutture:**
![[IMG_92FC2C84BF7D-1.jpeg]]

```c
struct dict_item {
	char *k;	//key
	float v;	//value
}; typedef struct dict_item dict_item;

struct node {
	dict_item info;		// puntatore alla coppia di valori
	struct node *next;	// nodo successivo
}; typedef struct node node;

struct dict {
	node **a;	// array di nodi
	int n;		// dimensione
	int M;		// capacità delle dizionario
}; typedef struct dict dict;

```

#### **Funzioni:**

**Inizializzazione dizionario:**
- Input: Dimensione  dizionario 
- Output: Puntatore al dizionario
```c
dict dict_init(int M){ // M dimensione del dizionario
	dict d;
	d.a = malloc(sizeof(node*) * M);
	d.n = 0;
	d.M = M;
	for(int i = 0; i < d.M; i++){ 
	// inizialmente tutti gli elemnti sono uguali a NULL
		d.a[i] = NULL;
	}
	return d;
}
```
- Dizionario vuoto

**Funzione che modifica valore associato alla chiave o inserisce nuova coppia valore chiave  in posizione 0 se non è già presente:**
- Input: dizionario e puntatore alla chiave ed valore (dict_item)
- Output: void
```c
void dict_set(dict d, dict_item e){
	int p = h(d, e.k);		// indice posizione della chiave nell dizionario (calcolato con la funzione hash)
	node *nd;

	nd = dict_search(d, e.k); // cerca il nodo con chiave k
	if( nd != NULL ) {		  // se esiste
		nd->info.v = e.v;	  // aggiorna il valore
	} else {			  	  // se non esiste
		d.a[p] = in0(d.a[p], e); // inserisci il nodo in testa alla lista
		d.n ++;						
	}
}
```
- lo inseriamo in posizione iniziale perche ha il costo minore

**Funzione che inserisce in un nodo  lo associa a una coppia chiave valore (dict_item) :**
- Input: dizionario e puntatore alla chiave ed valore (dict_item)
- Output: void
```c
node *in0(node *nd, dict_item e){
	node *p = malloc(sizeof(node)); // allochiamo memoria x l'elmento
	
	p->info = e;
	p->next = nd;
	nd = p;
		
	return nd;
}

```

**Funzione che cerca la chiave in un dizionario e ne restituisce la posizione:**
- Input: Dizionario, chiave
- Output:
	1. ritorna il puntate al node contenente l'item del dizionario con chiave k
	2. NULL se tale chiave non è presente nel dizionario
```c
node *dict_search(dict d, char *k){
	
	int p = h(d, k);   // pos teoria dove dovrebbe essere k 
					   // se presente nel dizioanrio
	node *q = d.a[p];  // puntatore alla nodo in posizione p

	// cliclo che va avanti finche non scorre tuttu i nodi 
	// o finche non trova una chiave identica alla chiave inserita
	while( q != NULL && strcmp(k, q->info.k) != 0){
		q = q->next;
	}
	
	return q; // se k non è presente dizionario q = null
			  // se è nel dizionario q = pointer to node contenente k
}

```
oss: [[C strcmp Funcion]] confronta due stringhe

**:**
```c

```

**:**
```c

```

**Continuo:** [[L12 Programmazione dei Calcolatori (C Dizionari)]]
