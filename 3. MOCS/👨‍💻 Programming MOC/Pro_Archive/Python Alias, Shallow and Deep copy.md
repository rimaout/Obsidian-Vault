---
Created: 2023-11-29
Type: Programming Note
Programming Language: "[[Python MOC]]"
Related:
  - "[[Python Lists]]"
  - "[[Python Data Types#Mutable and Unmutable data types|Python Mutable and Unmutable datatypes]]"
Completed: true
---
---
## Index
1. [[#Alias]]
2. [[#Shallow copy vs Deep copy]]
3. [[#Shallow copy vs Deep copy (unmutable objects)]]
	- [[#Unmutable not compound object]]
	- [[#Unmutable object compound by unmutable objects]]
	- [[#Unmutable object compound by un mutable objects]]
 4. [[#Shallow copy vs Deep copy (mutable objects)]]
	 - [[#Mutable not compound object]]
	 - [[#Mutable object compound by unmutable objects]]
	 - [[#Mutable object compound by un mutable objects]]

---
## Alias
- The *assignment* operator in python:
	- Doesn’t create a copy of the objects
	- It makes bindings between a variable and a object
		![[Screenshot 2023-11-30 at 11.53.24.png|500]]

**Partial example:**
``` python
a = [1,2,3]
b = a # y is an alias of x

a.append(4)
#a.out = [1,2,3,4]
#b.out = [1,2,3,4]

print(a is b) #Output: True

a = 1
#a.out = 1
#b.out = [1,2,3,4]

print(a is b) #Output: False
```

![[Pasted image 20231202183940.png|1100]]

---
## Shallow copy vs Deep copy
**Shallow copy:** Create a new object and insert references into the new object pointed at those found in the original.

**Deep copy:** Create a new object, and then recursively insert redundant copies of the objects found in the original.

---
## Shallow copy vs Deep copy ([[Python Data Types#Mutable and Unmutable data types|unmutable objects]])

> [!warning] Oss:
>There isn't any difference between alice, shallow copy and deep copy of an unmutable object

#### Unmutable not compound object

```python
import copy

x = "hello world"

alias = x
shallow = copy.copy(x)
deep = copy.deepcopy(x)

#test is x?
print(alias is x)   #Output: True
print(shallow is x) #Output: True
print(deep is x)    #Output: True

# x edit test
x += '!' # you can't modify an unmutable object, 
          # so the new x is a different object than the old x
print(alias is x)   #Output: False
print(shallow is x) #Output: False
print(deep is x)    #Output: False
```

![[Pasted image 20231202184034.png]]

#### Unmutable object compound by unmutable objects
``` python
import copy

x = ((1), 2)

alias = x
shallow = copy.copy(x)
deep = copy.deepcopy(x)

#test is X?
print(alias is x)   #Output: True
print(shallow is x) #Output: True
print(deep is x)    #Output: True

# x[1] += 1 -> error
#you can't use an assignment operator on a tuple item 
#so it's impossible to edit it
```

![[Pasted image 20231202184218.png|700]]

#### Unmutable object compound by un mutable objects:
``` python
import copy

x = ([1], {3})

alias = x
shallow = copy.copy(x)
deep = copy.deepcopy(x)

#test is x?
print(alias is x)   #Output: True
print(shallow is x) #Output: True
print(deep is x)    #Output: False

# test is x[0]
print(alias[0] is x[0])   #Output: True
print(shallow[0] is x[0]) #Output: True
print(deep[0] is x[0])    #Output: False

#x item edit tedt
x[0].append(2), 
print(alias)   #Output: ([1, 2], {3})
print(shallow) #Output: ([1, 2], {3})
print(deep)    #Output: ([1], {3})

```
\
![[Pasted image 20231202184314.png|1100]]

---
## Shallow copy vs Deep copy ([[Python Data Types#Mutable and Unmutable data types|mutable objects]])

#### Mutable not compound object
```python
import copy

x = [1,1]

alias = x
shallow = copy.copy(x)
deep = copy.deepcopy(x)

# test is x?
print(alias is x)   #Output: True
print(shallow is x) #Output: False
print(deep is x)    #Output: False

# test is x[1]
print(alias[1] is x[1])   #Output: True
print(shallow[1] is x[1]) #Output: True
print(deep[1] is x[1])    #Output: True
 
# x edit test
x.append(3)
print(alias)    #Output: [1,1,3]
print(shallow)  #Output: [1,1]
print(deep)     #Output: [1,1]

# x item edit test
x[1] += 1
print(alias)    #Output: [1,2,3]
print(shallow)  #Output: [1,1]
print(deep)     #Output: [1,1]

# test is x[1]
print(alias[1] is x[1])   #Output: True
print(shallow[1] is x[1]) #Output: False
print(deep[1] is x[1])    #Output: False
```

![[Pasted image 20231202181416.png|1100]]

#### Mutable object compound by unmutable objects

```python
import copy

x = ["hello", 1] 

alias = x
shallow = copy.copy(x)
deep = copy.deepcopy(x)

# test is x ?
print(alias is x)   #Output: True
print(shallow is x) #Output: False
print(deep is x)    #Output: False

# test is x[0]
print(alias[0] is x[0])   #Output: True
print(shallow[0] is x[0]) #Output: True
print(deep[0] is x[0])    #Output: True

# test is x[1]
print(alias[1] is x[1])   #Output: True
print(shallow[1] is x[1]) #Output: True
print(deep[1] is x[1])    #Output: True

# x item edit test
x[0] += "!"     # you cant't edit a string so the result is a new sting
print(alias)    #Output: ['hello!', 1]
print(shallow)  #Output: ['hello', 1]
print(deep)     #Output: ['hello', 1]

# test is x[0]
print(alias[0] is x[0])   #Output: True
print(shallow[0] is x[0]) #Output: False
print(deep[0] is x[0])    #Output: False
```

![[Pasted image 20231203110450.png|1100]]

#### Mutable object compound by un mutable objects
```python
import copy

x = [[1], [2]]

alias = x
shallow = copy.copy(x)
deep = copy.deepcopy(x)

# test is x ?
print(alias is x)   #Output: True
print(shallow is x) #Output: False
print(deep is x)    #Output: False

# test is x[0]
print(alias[0] is x[0])   #Output: True
print(shallow[0] is x[0]) #Output: True
print(deep[0] is x[0])    #Output: False

# x edit test
x.append(4)
x[0].append(2)
x[1][0] += 1
print(alias)    #Output: [[1, 2], [3], 4]
print(shallow)  #Output: [[1, 2], [3]]
print(deep)     #Output: [[1], [2]]
```

![[Pasted image 20231203113050.png]]

