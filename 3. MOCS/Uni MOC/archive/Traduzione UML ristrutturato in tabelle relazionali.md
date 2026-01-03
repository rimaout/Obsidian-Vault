---
type: Uni Note
class: "[[Basi di Dati 2 (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2025-06-30T14:46
updated: 2025-06-30T16:36
---
## Introduzione

**Obiettivo**: generare lo schema relazionale (con vincoli) per la base dati partendo dal [[Ristrutturazione diagramma UML concettuale delle classi|diagramma delle classi UML ristrutturato]].

 **Metodologia:**
- Ogni classe si traduce in una tabella relazionale
- Ogni associazione si traduce in una tabella relazionale più vincoli di foreign key (oppure si accorpa nella tabella che traduce una delle classi coinvolte)
- I vincoli di molteplicità dei ruoli di associazione si traducono in vincoli di chiave, foreign key, o in vincoli esterni (solitamente vincoli di inclusione).

La difficoltà più grande consiste nel saper gestire le molteplicità delle associazioni.
- [[#Classi senza Molteplicità]]
- [[#Molteplicità senza vincoli]]
- [[#Vincoli di molteplicità massima 1]]
- [[#Vincoli di molteplicità minima 1]]
- [[#Caso Accorpamento]]

## Classi senza Molteplicità

![[Pasted image 20250630150812.png|700]]

Scrittura PostgreSQL:

```
CREATE TABLE Studente (
	matricola integer not null,
	nome varchar not null,
	genere Genere not null,
	primary key (matricola)
);

CREATE TABLE Corso (
	nome varchar not null,
	modalita Modalita,
	primary key (nome)
);
```

All'esame utilizziamo una scrittura più compatta:
- $\text{Studente(}\underline{\text{matricola:integert}} \text{, nome:varchar, genere:Genere)}$
- $\text{Corso(}\underline{\text{nome:varchar}},\text{modalita*: Modalita)}$

Dove:
- Gli attributi sottolineati compongono la chiave primaria
- Diamo per scontato che tutti gli attributi sono `not null`
- Per indicare che un attributo può essere `null` lo indiamo con $*$ 

## Molteplicità senza vincoli

>[!note] Caso 0..\* -- 0..\*
>
>![[Pasted image 20250630154025.png|800]]
>
>$\text{Studente(}\underline{\text{matricola:integer}}\text{, nome:varchar, genere:Genere)}$
>
>$\text{Corso(}\underline{\text{nome:varchar}}\text{, modalita}^{*}\text{ Modalita)}$
>
>$\text{esame(}\underline{\text{studente:integer}}\text{, }\underline{\text{corso:varchar}}\text{, voto:Voto})$
>- $\text{foreign key: studente ref. Studente(matricola)}$
>- $\text{foreign key: corso ref. Corso(nome)}$

## Vincoli di molteplicità massima 1

>[!note] Caso 0..\* -- 0..1
>
>![[Screenshot 2025-06-30 at 15.28.38.png|800]]
>
>$\text{insegna(}\underline{\text{docente:integer}}\text{, corso:varchar, da:Date)}$
>- $\text{other key: docente}$
>- $\text{foreign key: docente references Docente(matricola)}$
>- $\text{foreign key: corso references Corso(nome)}$

>[!note] Caso 0..1 -- 0..1
>
>![[Screenshot 2025-06-30 at 15.52.57.png|800]]
>![[Screenshot 2025-06-30 at 15.54.02.png]]

## Vincoli di molteplicità minima 1


>[!note] Caso 1..\* -- 0..\* 
>
>![[Pasted image 20250630155545.png|800]]
>
>![[Pasted image 20250630155655.png]]

>[!note] 1..\* -- 1..\*
>
>![[Pasted image 20250630160042.png]]

## Caso Accorpamento

>[!note] Caso 0..* -- 1..1
>
>![[Pasted image 20250630161056.png]]

>[!note] Caso 0..1 -- 1..1 {id}
>
>![[Pasted image 20250630160920.png]]

>[!note] Caso 0..* -- 0..1
>
>![[Pasted image 20250630163504.png]]