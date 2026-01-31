---
created: 2023-09-28
type: Programming Note
programming language: "[[Python MOC]]"
related: []
completed:
updated: 2026-01-31T13:32
---
---
# Indice
- [[#Numero massimo rappresentabile in Python]]
- [[#Comparazioni casi particolari]]
- [[#Operazioni]]
- [[#Floating point]]
- [[#index delle stringhe]]
- [[#index delle stringhe]]
- [[#Slicing Stringe]]

---
# Numero massimo rappresentabile in Python

- In Python anche se superiamo i limiti della nostra architettura (esempio 32bit) non otteniamo un [[Over-flow]].
- Python riesce a gestire numeri cosi grandi perché gli interi sono rappresentati non in un singolo blocco ma in una specie di lista. 
- *oss:* Solo per numeri interi, quindi per rappresentazioni di numeri enormi conviene scriverli in forma intera

# Comparazioni casi particolari
```python
print(1 == True)   #Output: True
print(0 == False)  #Output: True
```

```python
print(1 == 1.0000) #Output: True
```

---
# Operazioni
```python
x = 2 + 1.00
print(x) #Output: 3.00000
```
i float anno sempre la precedenza quindi il risultato sarà sempre un float

# Floating point 
Nei floating point c'è un problema di precisione e approssimazione nei numeri float con una parte decimale particolarmente grande
![[Screenshot 2023-09-28 at 16.38.23.png]]

---
# index delle stringhe 
[[Python Strings Index]]

```python
 +---+---+---+---+---+---+
 | P | y | t | h | o | n |
 +---+---+---+---+---+---+
 0   1   2   3   4   5   6
-6  -5  -4  -3  -2  -1
```



---
# funzione index
La funzione index restituisce la posizione iniziale di una sotto stringa in una stringa

**Esempio:**
```python
nome = "matteo"
sub = "teo"

start_sub = nome.index(sub)
print(start_sub) #Output: 2
```

**Oss:** per trovare la posizione finale possiamo sottrarre la posizione iniziale della sotto-stringa alle lunghezza della stringa

```python
end_sub = len(nome)-start_sub
print(end_sub) #Output: 4
```

---
# Slicing Stringe
[[Python String Slicing]]


