---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-05-07T15:21
updated: 2025-05-07T15:32
---
Linguaggio di riferimento per le basi di dati relazionali, non è ancora supportato totalmente dai DBMS commerciali, per questo esistono 3 classificazioni:
- Entry (simile a SQL-89)
- Intermediate SQL (gran parte implementata da DBMS)
- Full SQL (include molte caratteristiche non implementate)

# Data Definition Language

>**Case Insensitive***: in SQL non c'è differenza tra `ciao` e `Cioa`.

### Creazione di Database, Schemi e Tabelle

**Creazione Database:**

```
create database <nome> [opzioni]
```

**Creazione Schema:** 
```
create schema <nome> [opzioni]
```

**Creazione Tabella:** 

```
create create table [nome_schema .] nome_tabella (
	nome_attributo dominio [ vincoli di dominio ] ,
	nome_attributo dominio [ vincoli di dominio ] ,
	...
	nome_attributo dominio [ vincoli di dominio ] ,
	[ altri vincoli intra− relazionali ]
	[ vincoli inter− relazionali ]
)
```
