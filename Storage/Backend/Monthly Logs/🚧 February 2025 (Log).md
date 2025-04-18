---
created: 2025-02-26T10:23
updated: 2025-04-18T16:09
tags:
  - monthly-log
---
-- 🚧 work in progress, come back at the end of the month 🚧 --

Ho imparato a fare uno squash commit, ovvero consiste nel prendere tanti piccoli commit e unirli in uno solo.

Add esempio se vogliamo unire gli ultimi tre commit dobbiamo:

Runnare il seguente codice, per "eliminare" gli ultimi tre commit ma mantenendo le modifiche:

```shell
git reset --soft HEAD~3
```

>[!note] Approfondimento
>- `HEAD` è un puntatore che indica un commit (in una breach), e possibile cambiare la breach ed il commit a cui punta l'`HEAD` utilizzando `git checkout`.
>- `HEAD~3` significa "il commit che è 3 genitori fa rispetto al commit corrente". Il tilde `~` è usato per indicare il numero di genitori da risalire.
>- Il flag `--soft` indica che si vuole mantenere i cambiamenti apportati nei commit successivi, mentre `--hard` li cancellerebbe e `--mixed` (il default) li lascerebbe nel working directory, ma non nello staging area.
>  
> ***oss:*** si può usare `git log` per vedere le informazioni riguardanti l'`HEAD`.

Ed effettuare un commit unendo tutte le modifiche:

```shell
git add . 
git commit -m "scrivi un messaggio per il commit"
git push --force-with-lease origin <brench>
```

>⚠️ sostituire `<branch>` con il nome della branch su cui caricare le modifiche.

>[!note] Approfondimento
>- `git add .` aggiunge tutti i file modificati allo staging area
>- `git push --force-with-lease origin <brench>`  questo comando forza l'aggiornamento del repository remoto con il nuovo commit squashato, sovrascrivendo la commit history.

## Siena



---

>**See all the other monthly logs:** [[Monthly Logs#📦 Log Archive|📦 Log Archive]]
