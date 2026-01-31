---
created: 2023-05-02T14:29
updated: 2026-01-31T13:32
---
Academic Year: 2022-2023
Class: [[Programmazione Calcolatori (Class)]]
Created: March 13, 2023
Tag: [[C MOC]], [[Python Dictionaries in C]]
Type: #Uni/Lecture 

---
**Lezione Precedente:** [[L11 Programmazione dei Calcolatori (C Dizionari)]]


## Implementazione  dizionari in C stile python
**Si utilizzano le liste di trabocco**

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
- Input: Dimesione DIzionario
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

**Funzione ch modifica valore associato ala chiave o inserisce nuova coppia valore chiave in posizione 0 se non è già presente:**
- Input: dizionario e puntatore alla chiave ed valore (dict_item)
- Output: void
- se non ce abastanza spazio utiliziao la funzione resize() per aumentare la capacità del dizionario
```c
void dict_set(dict d, dict_item e){
	int p = h(d, e.k);		// indice posizione della chiave nel dizionario (calcolato con la funzione hash)
	node *nd;

	nd = dict_search(d, e.k); // cerca il nodo con chiave k
	if( nd != NULL ) {		  // se esiste
		nd->info.v = e.v;	  // aggiorna il valore
	} else {			  	  // se non esiste
		d.a[p] = in0(d.a[p], e); // inserisci il nodo in testa alla lista
		d.n ++;	// aumento contaore numero elementi 	
	}
}
dict dict_set(dict d, dict_item e){
	int p = h(d, e.k);   // indice posizione della chiave nel dizionario (calcolato con la funzione hash)
	node *nd;
	
	nd = dict_search(d, e.k);  // cerca il nodo con chiave k
	if( nd != NULL ) {         // se esiste
		nd->info.v = e.v;      // aggiorna il valore
	} else {                   // se non esiste
		d.a[p] = in0(d.a[p], e); // inserisci il nodo in testa alla lista
		d.n++;   // aumento contaore numero elementi 
	}
	
	if (d.n/d.M > 4){     // controllo rapporto ellemnti capacità   
		 d = dict_resize(d, d.M*2+1);  // ridimensionamento
	}
	
	return d;
}
```
- lo inseriamo in posizione iniziale perche ha il costo minore

**Funzione che inserisce in un nodo lo associa a una coppia chiave valore (dict_item):**
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

**Funzione che stampa un dizionario (mosrando la sua vera struttura):**
```c
void print_dict(dict d){
	int i;
	for (i = 0; i < d.M; i++){
		printf("%d ", i);
		print_llist(d.a[i]);
		printf("\n");
	}
}

void print_llist(node *nd){
	node *p = nd;
	
	while( p != NULL ){
		printf("(\"%s\", %f) ", p->info.k, p->info.v);
		p = p->next; /*equivalente a p = (*p).next */
	}
}
```

**Funzione Hash:**
- prende la chiave la divite in bite, facciamo l xor bit a bit di tutti i bite che compongono la chiave e esce un numero
* nostro utilizzo ritornare un indice del dizionario

```c
int h(dict d, char *k){

	int i = 0; 
	hash_val = 0; // inizializziamo valore hash
	
	while( k[i] != '\0') {	// finchè non abbiamo raggiunto la fine della stringa
		hash_val = hash_val ^ k[i]; // ^ = XOR
		i += 1;
	}
	
	return hash_val % d.M;	// ritorna l'indice (resto di hash_val diviso capacità dizionario ) del dizionario
}
```
**oss:** esistono funzione hash più avanzate che migliorano la distribuzione delgli elemnto negl'array

**Funzione di cancellazione di un elemnto del dizionario:**
Elimina dal dizionario l'elemento con chiave k (se esiste)
 * Restituisce 1 se k è una chiave, 0 altrimenti

- inpiut dizionario: dizonario e chiave
- output: 1 cancellazione avvenuta , 0 se chiave non presente nel dizionario
![[IMG_672D8E5FD8F0-1.jpeg]]

```c
int dict_del(dict d, char *k){
	int p = h(d, k);	// troviamo indice della chiave k
	node *x, *q = dict_search(d, k);	// troviamo il puntatore al nodo contenente la chiave k

	if( q == NULL){		// se la chiave non è presente nel dizionario
		return 0;
	}
	
	if (d.a[p] == q){  // cancellazione primo elemento
		d.a[p] = q->next;
	} else {	// cancellazione elemento generico
		x = d.a[p];
		while ( x->next != q ){ // ricerca elemento precedente a q
			x = x->next;	
		}
		x->next = q->next;
	}
	free(q);	// liberiamo la memoria occupata dal nodo
	d.n--; 		// decrementiamo il numero di elementi del dizionario
	
	return 1;	//cancellazione andata a buon fine}

```


**Funzione di ridimensionamento del dizoinario :**
Esempio: quando li rapporto tra dimensione e capaciità del dizionario diventa superiore a una costante (es 4) raddopiare capacità del dionario
**oss:** facendo ciò bisogna riposizionare tutti gli elemnti presenti nel dizionario, ricalcolando la loro posizione. Perche la funzione di hash si basa sulla capacità, quindi le vacchie posizioni degli elementi non vanno più bene.

```c
dict dict_resize(dict d0, int new_M){ // d0 = vecchio dizionario, new_M = nuova capacità
	dict d1 = dict_init(new_M);		// inizializzazione nuovo dizionario
	node *q;	// nodo temporaneo
	for (int i = 0; i < d0.M; i++){ // scorriamo il vecchio dizionario
		while(d0.a[i] != NULL){		// finchè non abbiamo raggiunto la fine della lista linkata
			dict_set(d1, d0.a[i]->info);
			/* cancello il primo nodo di d.a[i]*/
			q = d0.a[i];
			d0.a[i] = q->next; 
			free(q); // libero memoria
		}
	} 
	free(d0.a);
	return d1;
}
```

# Array Multidimensionali  (matrici0  )
**:**
```c

```