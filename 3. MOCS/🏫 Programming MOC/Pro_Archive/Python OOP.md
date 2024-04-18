---
Created: 2023-11-14
Type: Programming Note
Programming Language: "[[Python MOC]]"
Related: 
Completed: false
---
---
## Index
1. [[#Definition]]
2. [[#Example]]

 [[Python Objects and Classes]]
- [[Python Inheritance]] [link](https://www.programiz.com/python-programming/inheritance) [link2](https://www.programiz.com/python-programming/multiple-inheritance)
- [[Python Operator Overloading]]  [link](https://www.programiz.com/python-programming/operator-overloading)
- [[Python Iterators, __iter__ and __next__]] [link](https://www.programiz.com/python-programming/iterator)
- [[Python Generators]] [link](https://www.programiz.com/python-programming/generator)
- [[Python Closures]] [link](https://www.programiz.com/python-programming/closure)
- [[Python Decorators]] [link](https://www.programiz.com/python-programming/decorator)
- [[Python @property decorator]] [link](https://www.programiz.com/python-programming/property)


---
## Definition 
Python supports various programming styles, including object-oriented programming (OOP) through the use of **objects** and **classes**.

 Object-Oriented Programming (OOP) is **a computer programming model that organises software design around data or objects, rather than functions and logic**. 

It is a programming paradigm that relies on the concept of classes and objects. 

OOP is used to structure a software program into simple, reusable pieces of code blueprints called classes, which are used to create individual instances of objects.

An object can be defined as a data field that has unique attributes and behaviour.

---
## Example

- An object is any entity that has **attributes** and **behaviours**. 
- For example, a `parrot` is an object. It has:
	- **attributes:** name, age, color, etc.
	- **behaviour:** dancing, singing, etc.

``` python
class Parrot:

    # class attribute
    name = ""
    age = 0

# create parrot1 object
parrot1 = Parrot()
parrot1.name = "Blu"
parrot1.age = 10

# create another object parrot2
parrot2 = Parrot()
parrot2.name = "Woo"
parrot2.age = 15

# access attributes
print(f"{parrot1.name} is {parrot1.age} years old")
print(f"{parrot2.name} is {parrot2.age} years old")
```

**Output**
```
Blu is 10 years old
Woo is 15 years old
```

In the above example, we created a class with the name Parrot with two attributes: name and age.

Then, we create instances of the Parrot class. Here, parrot1 and parrot2 are references (value) to our new objects.

We then accessed and assigned different values to the instance attributes using the objects name and the `.` notation.

---