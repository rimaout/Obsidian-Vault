---
type: Uni Note
class: "[[Basi di Dati 2 (class)]]"
academic year: 2024/2025
related: 
completed: false
created: 2025-06-30T09:31
updated: 2025-06-30T14:50
---
## Introduzione

L'**obiettivo** finale è quello di trasformare il diagramma UML relativo alle classi e associazioni, in un nuovo diagramma equivalente, ma dalla cui struttura si possa direttamente derivare lo schema relazionale del DB.

La **metodologia** prevede una sequenza di passi da eseguire nell’ordine dato:
1. [[#Eliminazione di attributi Multivalore]]
2. [[#Tipi supportati dal DBMS|Sostituzione dei tipi di dato concettuali]] con opportuni tipi supportati dal DBMS (tipi base o definiti dall’utente)
3. [[#Ristrutturazione delle generalizzazioni tra Classi|Eliminazione delle generalizzazioni tra classi]]
4. [[#Ristrutturazione delle generalizzazioni tra Associazioni|Eliminazione delle generalizzazioni tra associazioni]]
5. [[#Identificatori di classe|Definizione di un identificatore per ogni classe]]
6. [[#Ristrutturazione dei Vincoli|Ristrutturazione dei vincoli]]
7. [[#Ristrutturazione delle Operazioni]]

### Eliminazione di attributi Multivalore

Creare una *nuova classe* le cui istanze rappresentano i valori del *tipo di dato* effettivamente utilizzate nel livello degli oggetti e dei link:

![[Screenshot 2025-06-30 at 10.08.25.png]]
![[Screenshot 2025-06-30 at 10.18.48.png]]

- Si utilizza sempre molteplicità `1..*` (DB dovrà memorizzare solo gli indirizzi email effettivamente associati ad (almeno) uno studente)
- E’ la molteplicità dell’attributo concettuale: `X..Y`
- L'`{id}`indica che non vogliamo rappresentare nel DB più volte la stessa istanza del tipo

>[!note] Output
>
>Al termine del passo di eliminazione degli attributi multivalore tutti gli attributi del diagramma ristrutturato hanno vincoli di cardinalità `[0..1]` oppure `[1..1]`.

### Tipi supportati dal DBMS

Scegliere un opportuno tipo di dato supportato dal DBMS per ogni attributo, anche definendo, tramite SQL, tipi di dato utente.

>[!note] Tipi concettuali base
>- Intero -> `integer`
>- Reale -> `real`
>- stringa -> `varchar(…)`
>- Data -> `Date`
>- Ora -> `Time`
>- DataOra -> `DateTime`
>- Istante di tempo -> `TimeStamp`

>[!note] Tipi Specializzati
>
>È possibile definire nuovi tipi di dato supportati dal DBMS usando SQL, specializzanto i tipi concettuali di base, attraverso `CREATE DOMAIN`.
>
>```sql
>CREATE DOMAIN Voto AS Integer:
>	CHECK (value >= 18 and value <= 31);
>```

>[!note] Tipi Composti
>
>È possibile definire nuovi tipi di dato composti supportati dal DBMS, usando SQL attraverso `CREATE TYPE … AS (...)`.
>
>In SQL ogni campo di un dato composte, deve essere contrassegnato `not null`. 
>
>```sql
>CREATE TYPE Indirizzo as:
>	via varchar(100) NOT NULL,
>	civico integer NOT NULL CHECK (value > 0)
>```
>
>Ma molti DBMS non implementano tutte le funzionalità di SQL, ad esempio [[PostgreSQL]] (il DBMS utilizzato per l'esame) non supporta l'utilizzo di `NOT NULL` o `CHECK` in `CREATE TYPE`, per questo dobbiamo utilizzare dei **domini ausiliari**.
>
>```sql
>CREATE Domain String100_not_null AS varchar(100)
>	CHECK (value IS NOT NULL);
>
>CREATE DOMAIN Int_gz_not_null AS Integer
>	CHECK (value IS NOT NULL and value > 0);
>
>CREATE TYPE Indirizzo as
>	via String100_not_null,
>	civico Int_gz_not_null
>```

>[!note] Tipi Enumerativi
>
>È possibile definire nuovi tipi di dato enumerativi supportati dal DBMS, usando SQL attraverso `CREATE TYPE … AS ENUM`.
>
>```sql
>CREATE TYPE ColorePrimario AS ENUM ('Rosso', 'Blu', 'Giallo');
>```

### Ristrutturazione delle generalizzazioni tra Classi

L'**obbiettivo** è ristrutturare il diagramma UML delle classi in uno equivalente che **non contenga** generalizzazione o relazioni-isa tra classi dato che non sono supportate dal DBMS.

**Metodologia** si scegliere il modo più opportuno per risolvere le generalizzazioni, scegliendo tra tre possibili approcci:
- ***Fusione*** di sottoclassi nelle loro superclassi
- ***Divisione*** delle superclassi in classi disgiunte
- ***Sostituzione*** di relazioni is-a con associazioni

>[!note]- Fusione
>
>**1 Sottoclasse**: fondere un intero livello della generalizzazione (superclasse + sottoclassi) in un’unica classe:
>
![[Pasted image 20250630114519.png|1200]]
>
>**Più Sottoclassi:**
>
>![[Pasted image 20250630115012.png|1200]]
>
>**Più Sottoclassi + Disjoint:**
>
>![[Pasted image 20250630114707.png|1200]]
>
>**Più Sottoclassi + Disjoint + Complete:**
>
>![[Pasted image 20250630114916.png|1200]]
>
>**Più Sottoclassi + Complete:**
>
>![[Pasted image 20250630115354.png|1200]]

>[!note]- Divisione
>
>La divisione può essere utilizzata in casi di sottoclassi disgiunte e complete:
>
>![[Pasted image 20250630120139.png|1200]]

>[!note]- Sostituzione
>
>Sostituiamo ogni generalizzazione con un associazione, ed si utilizzano dei vincoli per implementare eventuali disgiunzioni e completezze.
>
>**2 Classi:**
>
>![[Pasted image 20250630121749.png|1200]]
>
>**2 Classi + Disjoint:**
>
>![[Pasted image 20250630121902.png|1200]]
>
>**2 Classi + Complete:**
>
>![[Pasted image 20250630123403.png|1200]]
>
>**2 Classi + Disjoint + Complete:**
>
>![[Pasted image 20250630123446.png|1200]]

### Ristrutturazione delle generalizzazioni tra Associazioni

L'**obbiettivo** è ristrutturare il diagramma UML delle classi in uno equivalente che **non contenga** generalizzazione o relazioni-isa tra associazioni dato che non sono supportate dal DBMS.


**Metodologia** si scegliere il modo più opportuno per risolvere le generalizzazioni, scegliendo tra tre possibili approcci:
- ***Fusione*** di sotto-associazioni nelle loro super-associazioni, se opportuno a valle del passo precedente
- Aggiunta di ***vincoli esterni*** 

>[!note]- Fusione
>
>![[Pasted image 20250630134918.png|1200]]

>[!note]- Vincoli Esterni
>
>![[Pasted image 20250630135018.png|1200]]

### Identificatori di classe

L'**obbiettivo** consiste nel ristrutturare il diagramma UML delle classi in uno equivalente che abbia almeno un identificatore per ogni classe, che fungerà da chiave della futura tabella del DB, ed eleggere **un** **identificatore primario per ogni classe**, che lungherà da chiave primaria della futura tabella.

**Metodologia:**
- Per ogni classe con identificatori concettuali, decidere se uno tra quelli disponibili è di qualità sufficiente per formare una chiave primaria: non deve essere troppo complesso. Eleggerlo a identificatore primario.
- Per ogni classe senza identificatori concettuali, o per la quale non è stato scelto un identificatore primario al passo precedente, definire un **identificatore artificiale**.

![[Pasted image 20250630142522.png|1200]]

>[!note] Cicli
>
>![[Pasted image 20250630142721.png|1100]]

## Ristrutturazione dei Vincoli

**Obbiettivo:** Ristrutturare i vincoli derivati dal diagramma UML concettuale delle classi in vincoli equivalenti sul diagramma UML delle classi ristrutturato.

## Ristrutturazione  delle Operazioni

**Obbiettivo:** Ristrutturare la specifica di ogni operazione di classe, e di ogni operazione di use- case in modo da adattarla alla nuova struttura del diagramma UML delle classi ristrutturato.



