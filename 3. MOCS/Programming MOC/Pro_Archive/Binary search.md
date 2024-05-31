---
created: 2023-06-14
type: Programming Note
programming language: General
related:
  - "[[Search Algorithms]]"
completed: 
updated: 2024-05-27T13:29
---
---
**index:**
1. [[#Binary Search Definition]]
2. [[#Binary Search Working]]
3. [[#General Steps]]
4. [[#Iterative Method]]
5. [[#Recursive Method]]
6. [[#Binary Search Complexity]]

---
## Binary Search Definition 
Binary Search is a searching algorithm for finding an element's position in a **sorted array**.

- In this approach, the element is always searched in the middle of a portion of an array.
- Binary search can be implemented only on a sorted list of items. If the elements are not sorted already, we need to sort them first.

---
## Binary Search Working
Binary Search Algorithm can be implemented in two ways which are discussed below.

1. [[#Iterative Method]]
2. [[#Recursive Method]]

---
## General Steps
The general steps for both methods are discussed below.

1. The array in which searching is to be performed is:![[Screenshot 2023-06-14 at 15.13.30.png]]
	 Let `x = 4` be the element to be searched.

2. Set two pointers low and high at the lowest and the highest positions respectively:![[Screenshot 2023-06-14 at 15.14.50.png]]
    Setting pointers

3. Find the middle element mid of the array ie. `arr[(low + high)/2] = 6` ![[Screenshot 2023-06-14 at 15.15.40.png]]
    Mid element
    
4. If x == mid, then return mid. 

5. **Else If** `x > mid`, compare x with the middle element of the elements on the right side of mid. This is done by setting low to `low = mid + 1`.

6. **Else**, compare x with the middle element of the elements on the left side of mid. This is done by setting high to `high = mid - 1`.![[Screenshot 2023-06-14 at 15.18.36.png]]
    Finding mid element
    
7. Repeat steps 3 to 6 until low meets high.![[Screenshot 2023-06-14 at 15.19.07.png]]Mid element

8. `x = 4` is found.![[Screenshot 2023-06-14 at 15.19.55.png]]
	Found

---
## Iterative Method



---
## Recursive Method 



---
## Binary Search Complexity

**Time Complexities:**
- Best case complexity: `O(1)`
- Average case complexity: `O(log n)`
- Worst case complexity: `O(log n)`

**Space Complexity:**
- The space complexity of the binary search is `O(1)`.

---