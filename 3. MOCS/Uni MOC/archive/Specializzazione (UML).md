---
type: Uni Note
class: "[[Basi di Dati 2 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-03-18T09:25
updated: 2026-01-31T13:32
---
## Introduzione

In una generalizzazione, una sottoclasse non solo può avere proprietà aggiuntive rispetto alla super-classe, ma può anche **specializzare** le proprietà ereditate dalla super-classe.

## Specializzazione degli Attributi

In una sotto classe possiamo specializzare gli attributi della super classe, ovvero possiamo restringere il tipo:
- Super-classe `Reale` -> Sotto-classe `Intero` (*ammesso* ✅)
- Super-classe `Intero` -> Sotto-classe `Intero >= 2` (*ammesso* ✅)
- Super-classe `Intero` -> Sotto-classe `Reale` (*non ammesso* ❌, non abbiamo ridotto il tipo)

>[!example] Esempio
>
>![[Pasted image 20250312145827.png|800]]

## Specializzazione di Associazioni

Anche un association class, essendo una classe, può essere specializzata ed essere soggetta alle specializzazioni che effettuiamo sulle classi.

In particolare importante ricordare che le **molteplicità** delle associazioni devono essere sempre uguale restrittive, ovvero:
- Super-associazione `1..*` -> Sotto-associazione `2..*` (*ammesso* ✅)
- Super-associazione `1..*` -> Sotto-associazione `2..5` (*ammesso* ✅)
- Super-associazione `2..*` -> Sotto-associazione `1..1` (*non ammesso* ❌)

>[!example] Esempio
>
>![[Pasted image 20250312150605.png|600]]
>
>- Un `ArticoloNuovo` può partecipare ad un solo link `vend_nuovo` ma ad ad infiniti link `venditore`.
>- Ogni articolo è venduto da **almeno un** utente.
>- Gli articoli nuovi devono essere venduti da **almeno un** venditore professionale.

## Specializzazione di operazioni di classe

Anche le operazioni di classe possono essere oggetto di specializzazione nelle sottoclassi.

La segnatura dell’operazione nella sottoclasse deve essere **compatibile** con quella dell’operazione definita nella supercasse, ovvero:
- Stesso numero e tipo di argomenti
- Il tipo di ritorno dell’operazione nella sottoclasse è dello stesso tipo o un sotto-tipo di quello dell’operazione nella superclasse.

>[!example] Esempio
>
>![[Pasted image 20250318092108.png|900]]
>
>In questo esempio il prezzo di ogni articolo va calcolato perché influenzato da fattori che variano (numero di ardi nazione) questo viene fatto attraverso l'operazione `prezzo`.
>
>Da notare che non cambia l’intestazione de metodo `prezzo` nella sottoclasse (resta compatibile) ma *cambia la specifica*.

