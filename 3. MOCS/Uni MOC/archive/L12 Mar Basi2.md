---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-03-12T14:49
updated: 2025-03-12T16:01
---
# Operazioni

## Introduzione

Una classe UML può definire anche proprietà dinamiche, che si chiamano operazioni (in java metodi).

Le proprietà dinamiche sono valori calcolati ogni volta che servono, a partire dai valori di altre proprietà o attributi.

## Operazioni di Classe

Una operazione della classe `C` indica che su ogni oggetto (istanza) della classe `C` si può eseguire un calcolo per:
- calcolare un valore a partire da altri dati e operazioni
- effettuare cambiamenti di stato dell’oggetto (cioè per modificare le sue proprietà), dei link in cui è coinvolto e/o degli oggetti a questo collegati

>***oss:*** Il diagramma delle classi non definisce cosa calcolano le operazioni, né se e come modificano i dati. Ogni classe del diagramma con operazioni andrà affiancata da un documento di specifica che entra nel dettaglio

![[Screenshot 2025-03-12 at 14.41.43.png|450]]

>[!note] Sintassi
>
>```java
>nome_operazione(argomenti) : tipo_ritorno
>```
>- ***argomenti*** è una lista di elementi della forma `nome_argomento : tipo_argomento`
>- ***tipo_ritorno*** è il tipo del valore restituito dall’operazione
>
>Una operazione di classe può essere invocata *solo* su un oggetto della classe.


>[!note] Ereditarietà
>
>

# Specializzazione

In una generalizzazione, una sottoclasse non solo può avere proprietà aggiuntive rispetto alla super-classe, ma può anche **specializzare** le proprietà ereditate dalla super-classe, **restringendone il tipo**.

## Specializzazione degli Attributi

In una sotto classe possiamo specializzare gli attributi della super classe, ovvero possiamo respingere il tipo:
- Super-classe `Reale` -> Sotto-classe `Intero` (**ammesso**)
- Super-classe `Intero` -> Sotto-classe `Intero >= 2` (**ammesso**)
- Super-classe `Intero` -> Sotto-classe `Reale` (**non ammesso**, non abbiamo ridotto il tipo)

![[Pasted image 20250312145827.png|800]]

## Specializzazione di Associazioni

àòdjkslfjklsjgflkjflksajslgjalsjgljgljlgjaslfjglksajfgljal

![[Pasted image 20250312150605.png|600]]

>***oss:*** Un `ArticoloNuovo` può partecipare ad un solo link `vend_nuovo` ma ad ad infiniti link `venditore`.

## Specializzazione di operazioni di classe

