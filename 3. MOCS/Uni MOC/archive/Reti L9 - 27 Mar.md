---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-03-27T14:21
updated: 2025-04-10T11:29
---



## Numeri di sequenza e riscontro nello stop and wait

## Numeri di sequenza e riscontro nello stop and wait

Quando si invia un pacchetto e viene ricevuto correttamente dal destinatario c'è il rischio che il messaggio di conferma di ricezione che il destinatario invia al mittente non  arriva, di conseguenza il mittente ri invia il pacchetto questo porta ad avere tue pacchetti identici nel ricevente.

Se il meccanismo di sequenza de riscontro funziona corettamente questa sitazione non dovrebbe creare problemi.

## Protocolli con pipeline

Il meccanismo dello stop and wait non è capace di sfruttare al massimo la rete, per questo sono stati inventati una serie di protocolli che si basano su una pipeline.

**Pipelining**: il mittente ammette più pacchetti in transito, ancora da notificare.
- l’intervallo dei numeri di sequenza deve essere incrementato 
- buffering dei pacchetti presso il mittente e/o ricevente

Esistono due forme generiche di protocolli con pipeline:
- [[#Go back N]]
- [[#Finestra di ricezione]]

### Go back N



### Finestra di ricezione

>[!warning] Finestra di ricezione < finestra di invio
>
>![[Pasted image 20250327150102.png|500]]


## Ripetizione Selettiva 

Il mittente ri-invia soltanto i pacchetti per cui non ha ricevuto un acknowlegment.

Per fare ciò dobbiamo modificare la struttura della finestra del ricevente.

## Il migliore

Non esiste uno meccanismo migliore:
- [[#Finestra di ricezione]] è più leggero a livello di risorse ma se la conessione è congestionata rischi di aumentare drasticamente i pacchetti da spedire (molte ri-invii)
- [[#Ripetizione Selettiva]] se la connessione è congestionata , non rischi di aumentare drasticamente la congestione della rete ma è più pensate a livello di risorse sui nodi.
  
 