---
Created: 2023-09-23
Type: Programming Note
Programming Language: General
Related:
  - "[[Sorting Algorithms]]"
Completed: true
---
---
**index:**
1. [[#Bubble Definition]]
2. [[#Working of Bubble Sort]]
3. [[#Iterative Method]]
4. [[#Complexities]]

---
## Bubble Definition
- **Bubble sort** is a [[Sorting Algorithms]] that compares two adjacent elements and swaps them until they are in the intended order.

- Just like the movement of air bubbles in the water that rise up to the surface, each element of the array move to the end in each iteration. Therefore, it is called a bubble sort.

---

## Working of Bubble Sort

Suppose we are trying to sort the elements in **ascending order**.

**1. First Iteration (Compare and Swap)**
1. Starting from the first index, compare the first and the second elements.
2. If the first element is greater than the second element, they are swapped.
3. Now, compare the second and the third elements. Swap them if they are not in order.
4. The above process goes on until the last element

![[Screenshot 2023-06-14 at 15.30.18.png]]

**2. Remaining Iteration**

The same process goes on for the remaining iterations.

After each iteration, the largest element among the unsorted elements is placed at the end.![[Screenshot 2023-06-14 at 15.34.55.png]]
- In each iteration, the comparison takes place up to the last unsorted element.
- The array is sorted when all the unsorted elements are placed at their correct positions.

---
## Complexities
###### 1. Time Complexities

- **Worst Case Complexity:** `O(n2)`  
    If we want to sort in ascending order and the array is in descending order then the worst case occurs.
- **Best Case Complexity:** `O(n)`  
    If the array is already sorted, then there is no need for sorting.
- **Average Case Complexity:** `O(n2)`  
    It occurs when the elements of the array are in jumbled order (neither ascending nor descending).

###### 2. Space Complexity
- Space complexity is `O(1)` because an extra variable is used for swapping.
- In the **optimised bubble sort algorithm**, two extra variables are used. Hence, the space complexity will be `O(2)`.

---