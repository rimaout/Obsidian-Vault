---
created: 2024-04-11
type: Uni Note
class:
  - "[[Algoritmi 1 (class)]]"
academic year: 2023/2024
related:
completed: false
updated: 2026-01-31T13:32
---
---

>[!info] Index
>1. [[#Introduzione]]
>2. [[#Algoritmi $ Theta(n {2})$|O(n^2)]]
>3. [[#Algoritmi $ Theta(n log n)$|n log n]]
>4. [[#Algoritmi "Lineari"]]
>5. [[#Stable Sorting Algoritms]]

>[!info] Related
>- [[Algoritmi 1 (class)]]

---
## Introduzione

>[!danger] Teorema
>Gli algoritmi di ordinamento basiti sul confronto sono i più veloci e permettono di ordinare con un caso medio di $\theta(n\cdot \log n)$

##### Algoritmi $\Theta(n^{2})$
- [[Insertion Sort]] 🔴
- [[Selection Sort]] 🔴
- [[Bubble Sort]] 🔴

##### Algoritmi $\Theta(n \log n)$
- [[Marge Sort]] 🟢
- [[Quick Sort]] 🟢 (sistemare solo costo computazionale)
- [[Heap Sort]] 🟡 (da finire)

##### Algoritmi "Lineari"
- [[Bucket Sort]]

>[!warning] Non esistono algoritmi lineari
>- scrivi che non esistono algoritmi di ordinamento realmente lineari ma che i più veloci sono i n log n (che usano il confronto)

---
## Stable Sorting Algoritms 

Un algoritmo di ordinamento si dice stabile se mantiene l'ordine relativo per gli elementi che hanno chiavi uguali. In altre parole, se due elementi hanno la stessa chiave, un algoritmo di ordinamento stabile garantirà che l'elemento che compare prima nella lista originale venga posizionato prima nella lista ordinata.

Al contrario, un algoritmo di ordinamento non stabile può riordinare gli elementi con chiavi uguali in modo imprevedibile.

La stabilità è una proprietà utile in diversi contesti.
Ad esempio se si deve ordinare una lista rispetto a più chiavi, è possibile utilizzare un approccio noto come ordinamento stabile  iterato. L'idea è di effettuare l'ordinamento in modo iterativo, partendo dalla chiave meno significativa e procedendo gradualmente alla chiave più significativa. In questo modo, l'ordinamento finale rispetterà l'ordine relativo degli elementi anche rispetto alle chiavi meno significative.

---



