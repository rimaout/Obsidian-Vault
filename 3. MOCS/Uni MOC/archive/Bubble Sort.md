---
created: 2024-04-30T16:57
type: Uni Note
class:
academic year: 2023/2024
related:
completed: false
updated: 2026-01-31T13:32
---
---

>[!abstract] Index
>1. 

>[!abstract] Related
>- 

---
## Codice  

```python
def Bubble_Sort(Array):
  for i in range(len(Array)):
    for j in range(len(Array)-a, i, -1) # scorre da dx a sx
       if Array[j] < Array[j-1]:
        Array[j], Array[j-1] = Array[j-1], Array[j]
```

## Costo
$\sum_{i = 0}^{n-2} \, (n-1) \, \theta(1) = \theta(n^2)$

## Principio  
- che sia a partire da dx o da sx, ogni coppia di elementi adiacenti vengono confrontati, e vengono scambiati finchè non sono in ordine  
- quindi ogni iterazione del for esterno porta il minimo/massimo in posizione (a seconda che lo si sta scorrendo da dx o da sx) per poi passare al successivo elemento e così via  

- da destra verso sinistra x il minimo
- da sinistra verso  destra x il massimo
  
## Cose da sapere  
- Non usa memoria aggiuntiva  
- Non vi è differenza tra caso migliore e caso peggiore, l'algoritmo impiega sempre $\theta(n^2)$  
- È un algoritmo di ricerca stabile (ossia se vi sono varie occorrenze di elementi con stesso valore, vengono lasciate nell'ordine in cui si trovano ((solitamente vanno in coda o in testa (da verificare) )) )  
- Stable Sorting Algorithms:  
	- Insertion Sort  
	- Merge Sort  
	- Bubble Sort  
	- Counting Sort  

---