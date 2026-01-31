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
updated: 2026-01-31T13:32
---
---

>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Metodi]]

>[!abstract] Related
>- [[Alberi Binari (Struttura Dati)]]
>- [[Algoritmi 1 (class)]]

---
## Introduzione

Struttura che si basa su due Array:
>[!info] Array k (chiavi)
> Vettore che contiene i valori dei nodi dell'albero

>[!info] Array P (padri)
> Vettore che ha un corrispondenza biettiva tra gli n nodi dell'albero (l'array k) e gli indici $0,\dots,n-1$, l'elemento $P[i]$ del vettore $P$ contiene l'indice del padre del nodo $i$ nell'albero

>[!info] Esempio
>![[signal-2024-05-04-112338.png|600]]

## Metodi

**Leggi:** [[Operazioni su diverse rappresentazioni di alberi binari a confronto]]

---