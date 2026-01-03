---
created: 2023-11-22
programming language: "[[Python MOC]]"
type: Programming Note
related:
  - "[[Python OOP]]"
  - "[[Python Objects and Classes]]"
completed: true
updated: 2024-05-27T13:29
---
---
If you what to print the result of a fusions or generator that returns a objet you have to translate i to a list or tuple or set (ex: list(map) ,set(map) ...)

**Example:**
``` python
result = map(lambda x,y: (x.upper(),y.lower()),  ["jAx", "KeEpEr"], ["ToNy", "sTaRk"]))

print(result)         #Output: <map object at 0x1029989a0>
print(list(result1))  #Output: [('JAX', 'tony'), ('KEEPER', 'stark')]
print(tuple(result1)) #Output: (('JAX', 'tony'), ('KEEPER', 'stark'))
print(set(result1))   #Output: {('JAX', 'tony'), ('KEEPER', 'stark')}
print(dict(result1))  #Output: {'JAX': 'tony', 'KEEPER': 'stark'}

```