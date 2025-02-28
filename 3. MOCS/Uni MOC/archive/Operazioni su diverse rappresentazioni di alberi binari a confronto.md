---
created: 2024-05-04
type: Uni Note
class:
  - "[[Algoritmi 1 (class)]]"
academic year: 2023/2024
related:
  - "[[Alberi (Struttura Dati)]]"
  - "[[Alberi Binari (Struttura Dati)]]"
completed: true
updated: 2025-02-27T18:34
---
---

>[!abstract] Index
>1. [[#Trovare il Nodo Padre]]
>2. [[#Determinare numero di figli]]
>3. [[#Determinare distanza di un nodo dalla radice]]

>[!abstract] Related
>- [[Alberi Binari (Struttura Dati)]]
>- [[Rappresentazione posizionale (Alberi Binari)]]
>- [[Memorizzazione tramite puntatori (Alberi Binari)]]
>- [[Rappresentazione tramite vettore dei padri (Alberi Binari)]]

---
## Trovare il Nodo Padre

>[!warning] [[Memorizzazione tramite puntatori (Alberi Binari)|Struttura a puntatori]]
>Dobbiamo accedere all’albero tramite il puntatore alla sua radice, ma poi non possiamo scorrere la struttura come fosse una lista, perché non sappiamo se dirigerci a destra o a sinistra dovremo quindi imparare a navigare tra i nodi dell’albero (visita di alberi) . **(rivedere questa parte quando sai come navigare un albero a puntatori)**

>[!warning] [[Rappresentazione posizionale (Alberi Binari)|Rappresentazione posizionale]]
>Il padre del nodi $i$ è in posizione $\frac{i-1}{2}$.

>[!warning] [[Rappresentazione tramite vettore dei padri (Alberi Binari)|Vettore dei padri]]
>L'indice del padre di ogni nodo $i$ è memorizzato direttamente nell'elemento $P[i]$ del vettore.

---
## Determinare numero di figli

>[!warning] [[Memorizzazione tramite puntatori (Alberi Binari)|Struttura a puntatori]]
>Controllare i campi `.left` e `.right` di ogni nodo, se questi compi contengono dei puntatori diversi da `none` allora hanno dei figli

>[!warning] [[Rappresentazione posizionale (Alberi Binari)|Rappresentazione posizionale]]
>Dato un nodo in posizione $i$ se ha dei nodi figli dobbiamo accedei ai puntatori in posizione`2i+1` e `2i+2` e controllare se sono vuoti o no.

>[!warning] [[Rappresentazione tramite vettore dei padri (Alberi Binari)|Vettore dei padri]]
>Si deve scorrere l’intero vettore e contarvi il numero di occorrenze dell’elemento (l’indice del nodo di cui vogliamo contare i figli).

---
## Determinare distanza di un nodo dalla radice

>[!warning] [[Memorizzazione tramite puntatori (Alberi Binari)|Struttura a puntatori]]
>come nel caso della ricerca del padre di un nodo per farlo dovremo prima vedere come navigare tra i nodi dell’albero. **(rivedere questa parte quando sai come navigare un albero a puntatori)**

>[!warning] [[Rappresentazione posizionale (Alberi Binari)|Rappresentazione posizionale]]
> Il livello (ovvero la sua distanza dalla radice)  di un nodo in posizione $i$ è possibile calcolarla con questa formula $\log_{2} i$

>[!warning] [[Rappresentazione tramite vettore dei padri (Alberi Binari)|Vettore dei padri]]
>Partendo dal nodo in posizione $i$ risaliamo di padre in padre passando per `P[i]` poi per `P[P[i]]` poi per `P[P[P[i]]]` e cosi via fino a raggiungere la radice, (Questo procedimento richiede al massimo $h$ passaggi dove `h` è l'altezza dell'albero).

---