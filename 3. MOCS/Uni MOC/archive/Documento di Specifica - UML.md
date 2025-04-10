---
type: Uni Note
class: "[[Basi di Dati 2 (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2025-04-07T16:08
updated: 2025-04-08T09:07
---
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

>***oss:*** per ora per descrivere queste condizioni utilizziamo un linguaggio pedante in futuro utilizzeremo espressione logiche per rimuovere le ambiguità.

![[Pasted image 20250319154245.png|1000]]

>[!note] Pre-Condizioni
>Condizioni che devono essere soddisfatte affinché l'operazione possa essere invocata con successo, riguardano:
>- l'oggetto di invocazione
>- valori degli argomenti
>- altri oggetti del sitema

^ce8426

>[!note] Post-Condizioni
>
>- Definiscono il tipo di ritorno
>- Definizione delle modifiche all’insieme degli oggetti esistenti, creazione di nuovi oggetti o link, eliminazione di oggetti o link

^417c2a

>[!example] Esempio 
>
>Specifica informale (la specifica formale si fa in logica del primo ordine)
>
>![[Pasted image 20250319143849.png|900]]

## Specifica di use-case

Documento separato da accludere allo schema concettuale, è utilizzato per descrivere le operazioni più in generale (non quelle di classe).

>***oss:*** non si utilizza `this` perché il diagramma degli use-case non descrive le operazioni di classe ma a delle operazioni più generali.

>[!example] Esempio
>
>![[Screenshot 2025-04-07 at 12.22.35.png|700]]

## Specifica vincoli esterni

Alcuni requisiti potrebbero implicare vincoli sui dati/oggetti/link che sono non sono esprimibili nel diagramma delle classi e per questo di definiscono vincoli esterni.

Dei vincoli esterni vanno definiti nel documento specificando:
- Un **identificatore** univoco utilizzato per riferirsi al vincolo in altre parti dello schema, l'identificatore rispetta uno standard noi useremo `[V.classi_a_cui_il_vincolo_si_applica.nome_vincolo]`.
- Un **asserzione** che definisce le condizioni che devono essere soddisfatte dai link/oggetti affinché siano in una configurazione legale per i vincoli.

![[Pasted image 20250407160724.png|900]]

>[!note] Vincoli esterni nel diagramma delle classi
>
>Nel caso (frequente) in cui un vincolo esterno si applica naturalmente agli oggetti di una sola classe, è raccomandato definirlo nella specifica di quella classe piuttosto che nella specifica dei vincoli esterni.
>
>Con questo approccio, il documento “Specifica dei vincoli esterni” conterrà solo la definizione dei vincoli che non sono attribuibili a singole classi.
>
>![[Pasted image 20250407160749.png|800]]
