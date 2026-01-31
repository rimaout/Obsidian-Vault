---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2025-11-12T14:43
updated: 2026-01-31T13:32
---
## Introduzione

Se nel codice sono presenti dei ciclici con iterazioni (indipendenti), può essere molto sensato parallelizzarli

queste ultime sono spesso le operazioni più dispendiose, rendendo favorevole una loro parallelizzazione. OpenMP è in grado di parallelizzare esclusivamente i cicli for , è assolutamente necessario che il numero di iterazioni totali sia noto a priori. 

La direttiva


---

openMp deve sempre conoscere qual'è il numero di iterazione che un for effettuerà in modo tale che potrà suddividere le iterazione equamente su tutti i thread.

Questo significa che all'interno di un for non possono esserci dei  break, o return o operazioni che modificano l'index.

Invece l'exit si può fare perché chiude tutto il programma.

---

Questo codice non va bene perché ad ogni iterazione del ciclo più esterno, vengono creati i processi e alla fine di ogni iterazione vengono distrutti.
```c
for (int i=0; i<3; ++i) {
	# pragrma omp parallel fot
	for (int j=0; j<6; ++j) {
		c(i,j)
	}
}
```

Ci servirebbe proprio un modo per metterli a sleep e non distruggerli.


Per risolvere questo problema possiamo fare cosi:

```c
# pragma omp parallel num_thereads(theread_count)
for (int i=0; i<3; ++i) {
	# pragrma omp parallel for
	for (int j=0; j<6; ++j) {
		c(i,j)
	}
}
```

In questo caso vengono creati i theread al nel primo pragma è tutto il blocco successivo viene eseguito da tutti i thread, ma quando arrivano al socondo pragma `# pragrma omp parallel for` capiranno che dividersi il carico del for interno.