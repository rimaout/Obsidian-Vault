---
type: Uni Note
class:
  - "[[WASA (class)]]"
academic year: 2024/2025
related:
completed: false
created: 2025-09-25T14:21
updated: 2025-09-30T14:28
---
>[!note] Definizioni
>- *Commit:* un'istantanea del repository in un determinato momento.
>- *﻿﻿Branch:* una linea di sviluppo. È un insieme ordinato di commit.
>- *﻿﻿Merge:* l'azione di fondere due o più branch.
>- *﻿﻿Tag:* un'etichetta personalizzata allegata a un commit (solitamente utilizzata per il versionameto).
>- *﻿﻿Fork:* un nuovo repository che è una copia di uno esistente.
>- *﻿﻿Pull/Merge request:* una richiesta di unire il codice da un fork o branch al repository/branch padre

>[!note] Commit
>
> Un commit un'istantanea del repository in un determinato momento.
> 
> Ogni commit è univocamente identificato da un codice SHA1 (un algoritmo di hashing), questo algoritmo utilizza i seguenti campi:
>- ﻿﻿data+autore, data + committer
>- ﻿﻿commento (obbligatorio)
>- ﻿﻿0,1, 0 più genitori
>- ﻿﻿tree: hash di tutti (~) i file nel
>  
>Ogni commit si dice **content addressable** avvero la sua chiave di hash creata usando il contenuto del commit.
>


>[!note] Staging Area
>
>Un commit contiene un sottoinsieme delle modifiche effettuate, lo staging equivale all'operazione di sezione delle modifiche da inserire nel commit.
>
>![[Pasted image 20250925144223.png|800]]

>[!note] Tag
>
>Utilizzato per etichettare i commit, solitamente utilizzati per indicare le versioni del software.
>
>![[Pasted image 20250926184356.png|200]]

>[!note] Branch
>
>Un branch è una linea di sviluppo, ovvero una sequenza di commit collegati da un DAG che:
>- *punta sempre all'ultimo commit*
>- inizia dall'ultimo commit orfano (solitamente il primo commit del repo)
>  
>![[Pasted image 20250926183837.png|400]]
>  
>Solitamente utilizzate per lavorare in parallelo a più versioni.
>
>>***nota:*** il primo commit crea il primo branch

>[!note] Head
>
>L’haed non è altro che il contenuto della nostra working directory, può puntare a un commit.
>
>![[Screenshot 2025-09-26 at 18.39.02.png|400]]
>
>Più in generale può puntare a un commit qualsiasi, a un branch (ultimo commit della branch) o a un tag (ovvero al commit associato a quel tag).
>
>Il `checkout` è l’operazione che ci permette di selezionale dove punta la head.

>[!note] Merge
>
>Operazione che fonde i cambiamenti tra due branch, in particolare si fa il merge da una brach `B` ad una branch `b`, dove l'originale `a` rimane invariate e la destinazione `A` conterrà i cambiamenti.
>
>Esistono tre strategie `fast forward`, `marge commit`, `rebase`, assumiamo di vare un merge di `B` in `A`
>
>**Fast Forward** - validiamo se il branch `B` è una continuazione di `A`:
>
>![[Pasted image 20250926185145.png|500]]
>
>**Branch Commit** - crea un nuovo commit con due genitori e punta al nuovo commit:
>
>![[Pasted image 20250926185219.png|400]]
>
>**Rebase** - effettua del revisionismo storico, ovvero automaticamente modifica la storia in modo che si lineare e r poi applica il fast-forward.
>- Ricrea ogni commit non in comune tra `A` e `B` dopo l'ultimo in `A` 
>  
>  ![[Pasted image 20250926184905.png|450]]
>  ![[Pasted image 20250926184920.png|600]]

---
## Come funziona










