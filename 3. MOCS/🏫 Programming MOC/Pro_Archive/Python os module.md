---
Created: 2023-06-26
Type: Programming Note
Programming Language: "[[Python MOC]]"
Related: 
Completed:
---
---
# Modulo os
Il modulo **os** fornisce gli strumenti per accedere a funzionalità dipendenti dal sistema operativo

---
## Funzioni

```python
os.listdir(directory_name)
```
si ottiene la lista di nomi (delle stringhe) dei file e cartelle nella cartella in input. 

``` 
os.getcwd(
```
si ottiene il nome della cartella corrente

```
os.listdir(os.getcwd())
```
ritorna la lista dei file della cartella corrente

---
# Sotto modulo Path
**path** implementa funzionalità per manipolare i percorsi nel file-system

---
## Funzioni

```python
os.path.isfile(x)
os.path.isdir(x)
```
restituiscono True se e solo se la stringa in input è, rispettivamente, il nome di un file o di una directory


```python
os.path.abspath(x)
```
restituisce il nome assoluto del file identificato dalla stringa x nella cartella corrente, vale a dire il nome completo del file a partire dalla cartella radice. La stringa risultante dipende, oltre che dalla posizione corrente e da x, dal sistema operativo.

```python
os.path.join(x, y, ...) 
```
crea un nome di un path unendo i path in input usando la convenzione del sistema operativo utilizzato.
**Esempio:**

```python
os.path.join(os.path.abspath('a_directory'), 'a_sub_directory', 'a_file.py')
```
n ambiente Linux o simili, la precedente chiamata restituirebbe una stringa del tipo: `/home/utente/a_directory/a_sub_directory/a_file.py'