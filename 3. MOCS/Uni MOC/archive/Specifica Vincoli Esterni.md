---
type: Uni Note
class: "[[Basi di Dati 2 (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2025-06-18T15:59
updated: 2025-06-18T16:07
---
## Introduzione 

Ci sono delle regole che il solo diagramma UML non può modellare, si definiscono quindi dei vincoli esterni al diagramma, in un documento separato, che hanno lo scopo di restringere il possibile livello degli oggetti, con dei requisiti più sofisticati.

![[Pasted image 20250407160724.png|1000]]

Un vincolo esterno è composto da:
- Un **identificatore** univoco per riferirsi al vincolo.
- Un’**asserzione** che definisce le condizioni che devono essere soddisfatte dai link/oggetti affinché siano in una configurazione legale per i vincoli.

>[!note] Vincoli esterni nel diagramma delle classi
>
>Nel caso (frequente) in cui un vincolo esterno si applica naturalmente agli oggetti di una sola classe, è raccomandato definirlo nella specifica di quella classe piuttosto che nella specifica dei vincoli esterni.
>
>Con questo approccio, il documento “Specifica dei vincoli esterni” conterrà solo la definizione dei vincoli che non sono attribuibili a singole classi.
>
>![[Pasted image 20250407160749.png|800]]