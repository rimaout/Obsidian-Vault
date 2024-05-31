---
created: 2023-11-16
type: Programming Note
programming language: "[[Python MOC]]"
related:
  - "[[Python Lists]]"
completed: false
updated: 2024-05-27T13:29
---
---
## Index
1. [[#Definition]]
2. [[#Functions]]
	- [[#Shape]]
	- [[#Create matrix]]

---
## Definition 
Bi-dimensional array organised by rows and column (list of lists)
``` python
matrix_2x1 = [ [0], [1] ] 

matrix_3x2 = [ [0,1], [1,2], [3,4] ] 
```

>[!example] Example:
> How to access an element of the matrix in the **third row** and  **second column** 
> `element = matrix[3][2]` 
> `element = matrix[r][c]`

---
## Functions 

### Shape
Function that calculates the number of row and columns of a matrix
```python
def shape(mat):
    # immediatly check empty matrix
    if len(mat) == 0 or len(mat[0]) == 0:
        return 0, 0

    r = len(mat) # Calculare number of rows
    c = len(mat[0]) # Calculate number of columns
    return r, c
```

### Create matrix

Function that generates an empty matrix or a matrix with the same value every where

```python
def create_matrix_long(r,c,value=0):
    # define matrix
    matrix = []
    # for each row
    for each_r in range(r):
        # define row
        row = []
        # for each col
        for each_c in range(c):
            # append the col to the row
            row.append(value)
        # append the row to the matrix
        matrix.append(row)
    return matrix    
```

```python
def create_matrix_short(r, c, value=0):
    '''
    a single for loop
    '''
    matrix = []
    for each_r in range(r):
        matrix.append([value] *c )
    return matrix
```

```python
def create_matrix_lc(r, c, value=0):
    '''
    with list comprehnsion
    '''
    return [ [value] * c for each_r in range(r) ]
```

```python
def create_matrix_map(r, c, value=0):
    '''
    with map and lambda function
    '''
    return list(map(lambda each_row: [value] * c, range(r)))
```

---
