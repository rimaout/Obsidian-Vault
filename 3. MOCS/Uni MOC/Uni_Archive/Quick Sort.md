---
Created: 2024-04-11
Type: Uni Note
Class: 
Academic Year: 2023/2024
Related: 
Completed: false
---
---

>[!info] Index
>1. 

---

### Equazione di Ricorrenza
$$
T(n) = T(n-1-k)+\theta(n)
$$

---
### Costo Temporale
**Caso Peggiore:** 
- $O(n^{2})$
- It occurs when the pivot element picked is either the greatest or the smallest element.    

>[!warning] oss
>This condition leads to the case in which the pivot element lies in an extreme end of the sorted array. One sub-array is always empty and another sub-array contains `n - 1` elements. Thus, quick-sort is called only on this sub-array.  

**Caso Migliore:** 
- $\Omega(n\cdot \log n)$
- It occurs when the pivot element is always the middle element or near to the middle element.

**Caso Medio:** 
- $\Theta(n\cdot \log n)$ 
- It occurs when the above conditions do not occur.

---