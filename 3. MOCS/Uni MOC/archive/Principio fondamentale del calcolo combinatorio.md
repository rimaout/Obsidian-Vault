---
type: Uni Note
class:
  - "[[Calcolo delle Probabilità (class)]]"
academic year: 2024/2025
related:
  - "[[Calcolo Combinatorio]]"
completed: true
created: 2024-10-01T10:34
updated: 2025-02-04T16:26
---

>[!abstract] Related
>- [[Calcolo Combinatorio]]
>- [[Calcolo delle Probabilità (class)]]

---
## Principio Fondamentale del Calcolo Combinatorio

>[!note] Principio 
>Si realizzino due esperimenti. Si supponga che il primo esperimento abbia $\textcolor{orange}{m}$ esiti possibili, che per ognuno di questi il secondo esperimento abbia $\textcolor{orange}{n}$ esiti possibili. 
>
>Allora, se **sequenze distinte di esiti** dei due esperimenti **producono esiti finali distinti**, i due esperimenti hanno in tutto $\textcolor{orange}{m\cdot n}$ esiti possibili.

>[!note] Principio Generalizzato
>Si realizzino $\textcolor{orange}{r}$ esperimenti. Si supponga che il primo esperimento abbia $\textcolor{orange}{n}$ esiti possibili, che per ognuno di questi il secondo esperimento abbia $\textcolor{orange}{n}$, esiti possibili, che per ognuno degli esiti dei due primi esperimenti il terzo esperimento abbia $\textcolor{orange}{n}$, esiti possibili ecc. 
>
>Allora, se sequenze distinte di esiti degli $\textcolor{orange}{r}$ esperimenti producono esiti finali distinti allora gli $\textcolor{orange}{r}$ esperimenti hanno in tutto $n_{1} \cdot n_{2}\cdot \dots \cdot n_{r}$ esiti possibili.

---
## Esempio

>[!example] Esempio 1
>Ci sono 10 mamme, ed ognuna ha 3 figli.
>Se si vuole eleggere una mamma e un suo figlio com mamma e figlio del anno quante possibilità si hanno?
>
>**Risposta:** Si può vedere la scelta della mamma come l'esito del primo esperimento e la scelta successiva di uno dei suoi bambini come l'esito del secondo esperimento; per il principio fondamentale vi sono 10 x 3 = 30 scelte possibili.
