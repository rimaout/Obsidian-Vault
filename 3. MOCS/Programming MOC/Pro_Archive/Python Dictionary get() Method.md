---
created: 2023-07-14
type: Programming Note
programming language: "[[Python MOC]]"
related:
  - "[[Python Dictionaries]]"
completed: true
updated: 2024-05-27T13:29
---
---
## Index
1. [[Python Dictionary get() Method#Definition|Definition]]
2. [[Python Dictionary get() Method#Syntax|Syntax]]
3. [[Python Dictionary get() Method#Parameter Values|Parameter Values]]
4. [[Python Dictionary get() Method#Return Values|Return Values]]
5. [[Python Dictionary get() Method#Python get() method Vs dict [key ] to Access Elements|Python get() Vs dict [key] ]]

---
## Definition 
The `get()` method returns the value of the item with the specified key.

---
## Syntax
``` python
dictionary.get(keyname, value)`
```

---
## Parameter Values

|Parameter|Description|
|---|---|
|_keyname_|Required. The keyname of the item you want to return the value from|
|_value_|Optional. A value to return if the specified key does not exist.  <br>Default value None|

---
## Return Values
- **If the key is found, get() returns:**
	- The *value related to key* if key is in the dictionary.

- **If the key is not found, get() returns:**
	- *None* if and value is not specified.
	- *Value parameter* if the key is not found and value is specified.


**Example:**
```Python
car = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}

x = car.get("model")
y = car.get("price", 15000)  
  
print(x) # OutPut: "Ford"
print(y) # OutPut: "15000"
```

---
## Python get() method Vs dict \[key\] to Access Elements

`get()` method returns a default value if the `key` is missing.

However, if the key is not found when you use `dict[key]`, `KeyError` exception is raised.

```python
person = {}

# Using get() results in None
print('Salary: ', person.get('salary'))


# Using [] results in KeyError
print(person['salary'])
```

**Output:**
```python
Salary:  None
Traceback (most recent call last):
  File "", line 7, in 
    print(person['salary'])
KeyError: 'salary'
```

---