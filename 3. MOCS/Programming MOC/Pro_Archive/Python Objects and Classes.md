---
created: 2023-11-14
type: Programming Note
programming language: "[[Python MOC]]"
related:
  - "[[Python OOP]]"
completed: true
updated: 2024-05-27T13:29
---
--
## Index
1. [[#Definition]]
2. [[#Classes]]
3. [[#Objects]]
4. [[#Access class attributes using Objects]]
5. [[#Python Methods]]
6. [[#Python Constructors]]

---
## Definition 
- An **object** is simply a *collection of data* (variables) and *methods* (functions). 
- A **class** is a *blueprint for that object*.

---
## Classes
**Syntax:**
``` python
class ClassName:
    # class definition 
```

*Example:*
``` python
class Bike:
    name = ""
    gear = 0
```
- `Bike` - the name of the class
- `name/gear` - variables inside the class with default values `""` and **0** respectively.

>[!Note] 
>The variables inside a class are called attributes.

---
## Objects 
An object is called an instance of a class. For example, suppose `Bike` is a class then we can create objects like `bike1`, `bike2`, etc from the class.

**Syntax:** 
```
objectName = ClassName()
```

*Example:*
``` python
# create class
class Bike:
    name = ""
    gear = 0

# create objects of class
bike1 = Bike()
```
Here, `bike1` is the object of the class. Now, we can use this object to access the class attributes.

---
## Access class attributes using Objects
We use the `.` notation to access the attributes of a class. 
```python
# modify the name attribute
bike1.name = "Mountain Bike"

# access the gear attribute
bike1.gear
```

---
## Python Methods
We can also define a function inside a Python class. A [[Python Function]] defined inside a class is called a method.

*Example:*
```python 
# create a class
class Room:
    length = 0.0
    breadth = 0.0
    
    # method to calculate area
    def calculate_area(self):
        print("Area of Room =", self.length * self.breadth)

# create object of Room class
study_room = Room()

# assign values to all the attributes 
study_room.length = 42.5
study_room.breadth = 30.8

# access method inside class
study_room.calculate_area()
```

**Output**:
```
Area of Room = 1309.0
```

---
## Python Constructors

Earlier we assigned a default value to a class attribute,

``` python
class Bike:
    name = ""
...
# create object
bike1 = Bike()
```

However, we can also initialise values using the constructors. For *example:*

``` python
class Bike:

    # constructor function    
    def __init__(self, name = ""):
        self.name = name

bike1 = Bike()
```

Here, `__init__()` is the constructor function that is called whenever a new object of that class is instantiated.

The constructor above initializes the value of the name attribute. We have used the `self.name` to refer to the name attribute of the `bike1` object.

If we use a constructor to initialize values inside a class, we need to pass the corresponding value during the object creation of the class.

```python
bike1 = Bike("Mountain Bike")
```

Here, `"Mountain Bike"` is passed to the name parameter of `__init__()`.

---