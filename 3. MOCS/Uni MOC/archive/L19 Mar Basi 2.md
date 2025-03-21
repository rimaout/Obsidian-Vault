---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-03-19T14:07
updated: 2025-03-19T17:48
---
## Introduzione

I diagrammi degli use-case modellano le **funzionalità** che il sistema deve realizzare, in termini di **use-case** (scenari di utilizzo), si basa su due concetti centrali:

>[!note] Use-case
Cattura un **insieme omogeneo di funzionalità** accedute da un **gruppo omogeneo di utenti**. 
>
>Tipicamente coinvolge concetti rappresentati da più classi e associazioni del diagramma delle classi.

>[!note] Attore


## Diagramma

Un diagramma UML degli use-case è un grafo in cui:

**Nodi** -  rappresentano attori e gli use-case

**Archi** - rappresentano:
- la possibilità per un attore di invocare uno use-case
- la possibilità per uno use-case di invocare un altro use-case
- la generalizzazione tra attori e tra use-case

## Associazione

![[Pasted image 20250319141945.png|500]]

## Dipendenze

>[!note] Inclusione
>

>[!note] Estensione
>

## Generalizzazione

>[!note] Generalizzazione tra use-case

>[!note] Generalizzazione tra attori

# Specifica 

## Specifica tipi di dato

Documento separato da accludere allo schema concettuale, utilizzato per definire [[Tipi di dato (UML)|tipi di dati non di default]].

>[!example] Esempio
>
>![[Pasted image 20250319143033.png|700]]

## Specifica di classe

Documento separato da accludere allo schema concettuale in cui vengono specificate:
- La descrizione della classe
- Specifica delle operazioni

La specifica di un operazione è composta da:
- *Intestazione* ovvero `nome_operazione( input1 : tipo1, input2 : tipo2 ... ) tipo_output`
- [[#^ce8426|Pre-condizioni]]
- [[#^417c2a|Post-condizioni]]

![[Pasted image 20250319154245.png|1000]]

>[!note] Pre-Condizioni
>Condizioni che devono essere soddisfatte affinché l'operazione possa essere invocata con successo, riguardano:
>- l'oggetto di invocazione
>- valori degli argomenti
>- altri oggetti del sitema

^ce8426

 
>[!note] Post-Condizioni

^417c2a

>[!example] Esempio 
>
>Specifica informale (la specifica formale si fa in logica del primo ordine)
>
>![[Pasted image 20250319143849.png|900]]

## Specifica di use-case


non si utilizza this perché il diagramma degli usa case non descrive le operazioni di classe ma a delle operazioni più generali 


## Specifica vincoli esterni

Un vincoli esterni vanno definiti nel documento specificando:
- Un **identificatore** univoco utilizzato per riferirsi al vincolo in altre parti dello schema, l'identificatore rispetta uno standard noi useremo `[V.classi_a_cui_il_vincolo_si_applica.nome_vincolo]`.
- Un **asserzione** che definisce le condizioni che devono essere soddisfatte dai link/oggetti affinché siano in una configurazione legale per i vincoli.

