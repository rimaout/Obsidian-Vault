---
Created: 2023-06-26
Academic Year: 2022/2023
Class:
  - "[[Programmazione Calcolatori (Class)]]"
Type: Uni Note
Programming Language: "[[Python MOC]]"
Related: 
Completed: true
---
---
# Index:
1. [[#Complessità Temporale]]
2. [[#Complessità Spaziale]]

---
# Complessità Temporale 

### Complessità di alcune funzioni Python più comuni

- Riassumiamo le complessità di alcune operazioni sulle strutture dati *lista*, *tuple*, *stringa*, *dizionario* e *set*. 
- Con **n** viene indicato il **numero di elementi nella struttura** a ovvero n = len(a).

- Viene indicato sia il costo nel caso peggiore che quello nel caso medio. 

>[!warning] Costo nel caso medio 
> - è il costo nel caso peggiore di n ripetizioni della stessa operazione diviso per n. 
> -  **Esempio:** sappiamo che l'operazione `append` ha una complessità nel *caso peggiore O(n)*, ma sappiamo anche che se eseguiamo n operazioni consecutive di append, una di queste avrà costo lineare mentre tutte le altre avranno costo costante. Quindi, siano `c0` e `c1` due opportune costanti, il costo delle n operazioni di append sarà: `(n-1)c0 + n*c1 = n(c0+c1) - c0 `
> - Dividendo tutto per n si ottiene il *costo medio* di una operazione che risulterà *O(1)*.

**Liste, tuple, e stringhe:**

|Operazione|Costo caso peggiore|Costo caso medio|
|---|---|---|
|*Indicizzazione*|O(1)|O(1)|
|*Memorizzazione°*|O(1)|O(1)|
|*Lunghezza*|O(1)|O(1)|
|*Accodamento°*|O(n)|O(1)|
|*Confronto*|O(n)|O(n)|
|*Cancellazione°* |O(n)|O(n)|
|*Copia*|O(n)|O(n)|
|*Inversione*|O(n)|O(n)|
|*Iterazione*|O(n)|O(n)|
|*Ordinamento*|O(n log n)|O(n log n)|
|*Ricerca*|O(n)|O(n)|
|*Slicing \[n:k\]*|O(k-n)|O(k-n)|
|*Estensione*| O(n) |o(n)|
|*Concatenazione a+b*| O(a+b)|O(a+b)|
**oss:** Le operazioni contrassegnate con *°* sono esclusive delle liste.

**Info extra:**
		- *Costo slicing* = costo della clonazione di k-n (indifferentemente da caso peggiore o medio).
		- *Costo estensione* = costo di accodare n elementi (dove n è la dimensione delle iterabile da cui prendiamo gli elementi), esempio a.extended(b) dove n = len(b)

**Dizionari:**

|Operazione|Costo caso peggiore|Costo caso medio|
|---|---|---|
|*Indicizzazione*|O(n)|O(1)|
|*Memorizzazione*|O(n)|O(1)|
|*Lunghezza*|O(1)|O(1)|
|*Cancellazione*|O(n)|O(1)|
|*Iterazione*|O(n)|O(n)|
|*Ricerca*|O(n)|O(1)|

**Set:**

|Operazione|Costo caso peggiore|Costo caso medio|
|---|---|---|
|*Inserimento*|O(n)O(1)|
|*Ricerca*|O(n)|O(1)|
|*Inserimento*|O(n)|O(1)|
|*Iterazione*|O(n)|O(n)|
|*Lunghezza*|O(1)|O(1)|
|*Unione*|||
|*Intersezione*|||
|*Differenza*|||

---
# Complessità Spaziale

- La complessità spaziale di un programma (funzione o frammento di codice), indica la *quantità di spazio utilizzato dal programma in funzione della dimensione dell'input*. 
- Anche in questo caso si può usare l'analisi del caso peggiore o medio e le notazioni asintotiche O-grande o Theta-grande.

>[!Warning]
> La complessità spaziale si calcola **omettendo** lo spazio **occupato** dall'**input** e dall'**output**.

###### Cose da sapere:
- **Spazio occupato dal codice** è costante *O(1)* infatti non dipende dall'input
- L'**alias** di una variabile (anche esterna) occupa *O(1)*

###### Esempio 1:
```python
def prima_pari(a):
   '''
   Assume che a sia una lista di interi.
   Ritorna una nuova lista con gli elementi di a 
   in cui pari precedono i dispari
   '''
   pari = [x for x in a if x%2 == 0]
   dispari = [x for x in a if  x%2 == 1]
   return pari+dispari
```
Sia n il numero di elementi di a, lo spazio utilizzato dalla funzione è dato dallo spazio usato usato dall'ambiente della funzione, ovvero dalla somma delle dimensioni delle variabili utilizzate dalla funzioni, più lo spazio occupato dalla funzione stessa (la dimensione del codice). Questa quantità di memoria deve essere espressa in funzione di n. A tal proposito osserviamo che lo spazio occupato dal codice della funzione non dipende mai dalla dimensione dell'input, pertanto si assume costante, ovvero O(1). Ora prendiamo in rassegna le variabili per ricavare lo spazio utilizzato dall'ambiente.
	
- **a** è alias della lista originale, quindi occupa lo spazio di un riferimento in memoria, ovvero *O(1)*
- la variabili **pari** e **dispari**: sono due nuove liste che, *insieme, contengono tutti gli elementi della lista originale*; questi sono interi quindi ognuno occupa uno spazio indipendente da n (costante), pertanto la dimensione delle due liste è *O(n)*
- la funzione restituisce una **concatenazione** delle due liste, questa operazione crea una copia che richiede *O(n)* spazio.

**Quindi:** la complessità temporale della funzione è *O(n)*.
i
###### Esempio 2:
```python
def prima_pari(a):
   ris = []
   for x in a:
       if x%2 == 0:
           ris.append(x)
   for x in a:
       if x%2 == 1:
           ris.append(x)
   return ris
```
- Anche in questo caso la **dimensione di ris** è *O(n)* quindi anche questa versione ha ***complessità spaziale O(n)***

- Si osservi però che, poiché il risultato deve essere una nuova lista di dimensione n, ogni soluzione non può avere complessità spaziale inferiore a O(n)

- La **seconda soluzione** *non utilizza liste di appoggio* ma soltanto la lista che verrà restituita in output, quindi è evidente che questa *soluzione è più efficiente* della prima ma questo non si evince dall'analisi asintotica. Ma se dal computo dello spazio occupato sottraessimo quello (necessario) utilizzato per l'input e per l'output otterremmo che la prima soluzione manterrebbe un costo O(n) per via delle liste d'appoggio pari e dispari, mentre la seconda soluzione avrebbe complessità spaziale O(1).

## Complessità Spaziale Funzioni Ricorsive

```python
def somma(n):
   '''
   Assume n intero non negativo
   '''
   if n == 0:
       return 1
   else:
       return n+somma(n-1)
```
- Questa funzione restituisce la somma dei primi n interi positivi. 

- La singola chiamata della funzione richiede spazio O(1), ovvero quello richiesto dalla variabile n e dalla memorizzazione della funzione. 

- Tuttavia, la chiamata somma(n) crea uno stack frame (o ambiente) che resta aperto fintanto che non viene restituito il risultato dalla chiamata di somma(n-1) che a sua volta crea un nuovo stack frame per somma(n-2) e così via fino all'invocazione di somma(0) che fa terminare la catena liberando la memoria di tutti i frame aperti.
 
- In **numero massimo di frame** aperti in contemporanea è proprio *n*, ciascuno di questi occupa una quantità di memoria costante e quindi la **complessità spaziale** di somma(n) è *O(n)*.