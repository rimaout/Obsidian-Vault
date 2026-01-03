---
created: 2023-03-30
type: Programming Note
programming language: "[[C MOC]]"
related: 
completed: true
updated: 2024-05-27T13:29
---
---

An array is a [variable](C%20Variables%20And%20Constants.md) that can store multiple values

## Syntax
```c
dataType arrayName[arraySize]
```

>[!warning]
>It's important to note that the size and type of an array cannot be changed once it is declared.

**Example:**
```c
float arr[5];
```

---
## Access Array Elements
You can access elements of an array by **indices**.
![[Pasted image 20230330081708.png]]

#### **Few keynotes**:

- Arrays have 0 as the first index
	- If arr size = `n`, last element index = `n-1`

- Suppose the starting address of `arr[0]` is **2120d**
- The address of the `mark[1]` will be **2124d** (+4)
- The address of `mark[2]` will be **2128d** (+4)
	- This is because the size of a `float` is 4 bytes.

Learn about [[C Memory Address]]

---

## How to initialize an array?

It is possible to initialize an array during declaration
```c
int arr[5] = {19, 10, 8, 17, 9};
```

You can also initialize an array like this
```c
int arr[] = {19, 10, 8, 17, 9};
```
Here, we haven't specified the size. However, the compiler knows its size is 5 as we are initializing it with 5 elements.

![[Pasted image 20230330081735.png]]

---

## Change Value of Array elements

```c
int arr[5] = {19, 10, 8, 17, 9}

// make the value of the third element to -1
arr[2] = -1;

// make the value of the fifth element to 0
arr[4] = 0;
```

---

## Input and Output Array Elements

Here's how you can take input from the user and store it in an array element.
```c
// take input and store it in the 3rd element
​scanf("%d", &mark[2]);

// take input and store it in the ith element
scanf("%d", &mark[i-1]);
```

Here's how you can print an individual element of an array.
```c
// print the first element of the array
printf("%d", mark[0]);

// print the third element of the array
printf("%d", mark[2]);

// print ith element of the array
printf("%d", mark[i-1]);
```

### Access elements out of its bound!
```c
int testArray[10];
```
You can access the array elements from `testArray[0]` to `testArray[9]`.

Now let's say if you try to access `testArray[12]`. The element is not available. This may cause unexpected output (undefined behavior). Sometimes you might get an error and some other time your program may run correctly.

Hence, you should never access elements of an array outside of its bound.

---

## Loop Through an Array

You can loop through the array elements with the `for` loop.

The following example outputs all elements in the `myNumbers` array:
**Example:**
```c
int myNumbers[] = {25, 50, 75, 100};  
int i;  
  
for (i = 0; i < 4; i++) {  
  printf("%d\n", myNumbers[i]);  
}
```

---
