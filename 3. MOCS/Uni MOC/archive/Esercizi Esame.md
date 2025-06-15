---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-06-12T19:38
updated: 2025-06-12T19:38
---






1. parte a 0.8 ma collide con i pacchetti 2,3,4 
2. parte a 1.2 ma collide con i pacchetti 1,2,3,4  
3. parte a 1.6 ma collide con i pacchetti 1,2,3,4,5
4. parte a 1.8 ma collide con i pacchetti 1,2,3,4,5,6
5. parte a 2.4 ma collide con i pacchetti 2,3,4,5,6,7
6. parte a 2.8 ma collide con i pacchetti 4,5,6,7
7. parte a 3.2 ma collide con i pacchetti 5,6
8. parte a 4.8 e non collide con nessun pacchetto, quindi arriva con successo alla destinazione

**Ragionamento:** il pacchetto 6 essendo partito a 2.8 è vulnerabile da tutti i pacchetti inviati nel range `[2.8-1, 2.8+1]` ovvero i pacchetti:
- 4: inviato a 1.8
- 5: inviato a 2.4
- 6: inviato a 2.8
- 7: inviato a 3.2

- La trasmissione del pacchetto **1** inizia a `1.0` e viene trasmesso con successo (non essendoci altri pacchetti trasmessi nello stesso slot).
- La trasmissione dei pacchetti **2,3,4** inizia a `2.0`, e sono in collisione tra loro.
- La trasmissione dei pacchetti **5, 6** inizia a `3.0`, e sono in collisione tra loro.
- La trasmissione del pacchetto **7** inizia a `4.0` e viene trasmesso con successo (non essendoci altri pacchetti trasmessi nello stesso slot).
- La trasmissione del pacchetto **8** inizia a `5.0` e viene trasmesso con successo (non essendoci altri pacchetti trasmessi nello stesso slot).


Per il pacchetto `1`:
- Viene effettuato il carrier sensing in `t = 0.8` ed il canale è vuoto quindi la sua trasmissione inizia in `t = 0.8`. 
- Quindi la sua trasmissione va da `0.8` a `1.8`.
- Allora gli altri nodi potranno ricevere la sua trasmissione da `1.2` a `2.2`.

Per il pacchetto `2`:
- Viene effettuato il carrier sensing in `t = 1.2` e determina che il canale non è vuoto dato che la trasmissione del pacchetto 1 è "percepita" da `1.2` a `2.2`.
- Quindi non viene trasmesso, dato che il canale non è vuoto.

Per il pacchetto `3`:
- Viene effettuato il carrier sensing in `t = 1,6` e determina che il canale non è vuoto dato che la trasmissione del pacchetto 1 è "percepita" da `1.2` a `2.2`.
- Quindi non viene trasmesso, dato che il canale non è vuoto.

Per il pacchetto `4`:
- Viene effettuato il carrier sensing in `t = 1,8` e determina che il canale non è vuoto dato che la trasmissione del pacchetto 1 è "percepita" da `1.2` a `2.2`.
- Quindi non viene trasmesso, dato che il canale non è vuoto.

Per il pacchetto `5`:
- Viene effettuato il carrier sensing in `t = 2.4` ed il canale è vuoto quindi la sua trasmissione inizia in `t = 2.4`. 
- Quindi la sua trasmissione va da `2.4` a `3.4`.
- Allora gli altri nodi potranno ricevere la sua trasmissione da `2.8` a `3.8`.

Per il pacchetto `6`:
- Viene effettuato il carrier sensing in `t = 2.8` e determina che il canale non è vuoto dato che la trasmissione del pacchetto 5 è "percepita" da `2.8` a `3.8`.
- Quindi non viene trasmesso, dato che il canale non è vuoto.

Per il pacchetto `7`:
- Viene effettuato il carrier sensing in `t = 3.2` e determina che il canale non è vuoto dato che la trasmissione del pacchetto 5 è "percepita" da `2.8` a `3.8`.
- Quindi non viene trasmesso, dato che il canale non è vuoto.

Per il pacchetto `8`:
- Viene effettuato il carrier sensing in `t = 4.8` e determina che il canale è vuoto dato che l'ultima trasmissione (del pacchetto 5) è "percepita" da `2.8` a `3.8`.
- Quindi la sua trasmissione va da `4.8` a `5.8`.
- Allora gli altri nodi potranno ricevere la sua trasmissione da `5.2` a `6.2`.

I nodi trasmessi con successo sono `1`, `5`, e `8` dato che non avvengono collisioni.

---

## CSMA

Per il pacchetto `1`:
- Viene effettuato il carrier sensing in `t = 0.1` ed il canale è vuoto quindi la sua trasmissione inizia in `0.1` e termina a `1.1`.
- Gli altri nodi potranno ricevere la sua trasmissione da `0.5` a `1.5`.  

Per il pacchetto `2`:
- Viene effettuato il carrier sensing in `t = 0.9` e determina che il canale non è vuoto dato che la trasmissione del pacchetto 1 è rilevata da `0.5` a `1.5`.
- Quindi il pacchetto non viene trasmesso.

Per il pacchetto `3`:
- Viene effettuato il carrier sensing in `t = 1.1` e determina che il canale non è vuoto dato che la trasmissione del pacchetto 1 è rilevata da `0.5` a `1.5`.
- Quindi il pacchetto non viene trasmesso.

Per il pacchetto `4`:
- Viene effettuato il carrier sensing in `t = 1.8` ed il canale è vuoto quindi la sua trasmissione inizia in `1.8` e termina a `2.8`.
- Gli altri nodi potranno ricevere la sua trasmissione da `2.2` a `3.2`.  

Per il pacchetto `5`:
- Viene effettuato il carrier sensing in `t = 1.9`, da punto di vista del nodo il canale è vuoto dato che la trasmissione del pacchetto 4 sarà rilevabile da `2.2` a `3.2`. 
- La trasmissione del pacchetto inizia da `1.9` e termina a `2.9`, gli altri nodi potranno ricevere la sua trasmissione da `2.3` a `3.3`
- Quindi il pacchetto viene trasmesso ma avviene una collisione con il pacchetto 4.

Per il pacchetto `6`:
- Viene effettuato il carrier sensing in `t = 2.4` e determina che il canale non è vuoto dato che la trasmissione del pacchetto 4 è "percepita" da `2.2` a `3.2` e del pacchetto 5 da `2.3` a `3.3`.
- Quindi non viene trasmesso, dato che il canale non è vuoto.

Per il pacchetto `7`:
- Viene effettuato il carrier sensing in `t = 2.6` e determina che il canale non è vuoto dato che la trasmissione del pacchetto 4 è "percepita" da `2.2` a `3.2` e del pacchetto 5 da `2.3` a `3.3`.
- Quindi non viene trasmesso, dato che il canale non è vuoto.

Per il pacchetto `8`:
- Viene effettuato il carrier sensing in `t = 2.8` e determina che il canale non è vuoto dato che la trasmissione del pacchetto 4 è "percepita" da `2.2` a `3.2` e del pacchetto 5 da `2.3` a `3.3`.
- Quindi non viene trasmesso, dato che il canale non è vuoto.

Per il pacchetto `9`:
- Viene effettuato il carrier sensing in `t = 3.4` ed il canale è vuoto quindi la sua trasmissione inizia in `3.4` e termina a `4.4`.
- Gli altri nodi potranno ricevere la sua trasmissione da `3.8` a `4.8`.

Per il pacchetto `10`:
- Viene effettuato il carrier sensing in `t = 4.1` e determina che il canale non è vuoto dato che la trasmissione del pacchetto 9 è "percepita" da `3.8` a `4.8`.
- Quindi non viene trasmesso, dato che il canale non è vuoto.

Per il pacchetto `11`:
- Viene effettuato il carrier sensing in `t = 4.6` e determina che il canale non è vuoto dato che la trasmissione del pacchetto 9 è "percepita" da `3.8` a `4.8`.
- Quindi non viene trasmesso, dato che il canale non è vuoto.

**Risultato Finale:***
- Pacchetti non spediti: `2, 3, 6, 6, 8, 10, 11`.
- Pacchetti spediti con successo: `1, 9`.
- Nodi spediti ma che hanno avuto una collisione: `4, 5`.

## CSMA/CD


Per il pacchetto `1`:
- Viene effettuato il carrier sensing in `t = 0.1` ed il canale è vuoto quindi la sua trasmissione inizia in `0.1` e termina a `1.1`.
- Gli altri nodi potranno ricevere la sua trasmissione da `0.5` a `1.5`.  

Per il pacchetto `2`:
- Viene effettuato il carrier sensing in `t = 0.9` e determina che il canale non è vuoto dato che la trasmissione del pacchetto 1 è rilevata da `0.5` a `1.5`.
- Quindi il pacchetto non viene trasmesso.

Per il pacchetto `3`:
- Viene effettuato il carrier sensing in `t = 1.1` e determina che il canale non è vuoto dato che la trasmissione del pacchetto 1 è rilevata da `0.5` a `1.5`.
- Quindi il pacchetto non viene trasmesso.

Per il pacchetto `4`:
- Viene effettuato il carrier sensing in `t = 1.8` ed il canale è vuoto quindi la sua trasmissione inizia in `1.8` e termina a `2.8`.
- Gli altri nodi potranno ricevere la sua trasmissione da `2.2` a `3.2`.  

Per il pacchetto `5`:
- Viene effettuato il carrier sensing in `t = 1.9`, da punto di vista del nodo il canale è vuoto dato che la trasmissione del pacchetto 4 sarà rilevabile da `2.2` a `3.2`. 
- La trasmissione del pacchetto inizia da `1.9` e termina a `2.9`, gli altri nodi potranno ricevere la sua trasmissione da `2.3` a `3.3`
- Quindi il pacchetto viene trasmesso ma avviene una collisione con il pacchetto 4.

Collisione tra `4` e `5`:
- Il nodo che sta trasmettendo il pacchetto `5` si accorge della collisione in `t = 2.2` e termina la trasmissione.
- Quindi la trasmissione di `5` va da `1.9` a `2.2` e gli altri nodi ricevono la ricevono da `2.3` a `2.6`.
- Il nodo che sta trasmettendo il pacchetto `4` si accorge della collisione in `t = 2.3` e termina la trasmissione
- Quindi la trasmissione di `4` va da `1.8` a `2.3` e gli altri nodi ricevono la ricevono da `2.2` a `2.7`. 

Per il pacchetto `6`:
- Viene effettuato il carrier sensing in `t = 2.4` e determina che il canale non è vuoto dato che la trasmissione del pacchetto 4 è "percepita" da `2.2` a `3.2` e del pacchetto 5 da `2.3` a `3.3`.
- Quindi non viene trasmesso, dato che il canale non è vuoto.

Per il pacchetto `7`:
- Viene effettuato il carrier sensing in `t = 2.6` e determina che il canale non è vuoto dato che la trasmissione del pacchetto 5 è "percepita" da `2.2` a `3.2` e del pacchetto 6 da `2.3` a `3.3`.
- Quindi non viene trasmesso, dato che il canale non è vuoto.

Per il pacchetto `8`:
- Viene effettuato il carrier sensing in `t = 2.8` e determina che il canale non è vuoto dato che la trasmissione del pacchetto 5 è "percepita" da `2.2` a `3.2` e del pacchetto 6 da `2.3` a `3.3`.
- Quindi non viene trasmesso, dato che il canale non è vuoto.

Per il pacchetto `9`:
- Viene effettuato il carrier sensing in `t = 3.4` ed il canale è vuoto quindi la sua trasmissione inizia in `3.4` e termina a `4.4`.
- Gli altri nodi potranno ricevere la sua trasmissione da `3.8` a `4.8`.

Per il pacchetto `10`:
- Viene effettuato il carrier sensing in `t = 4.1` e determina che il canale non è vuoto dato che la trasmissione del pacchetto 9 è "percepita" da `3.8` a `4.8`.
- Quindi non viene trasmesso, dato che il canale non è vuoto.

Per il pacchetto `11`:
- Viene effettuato il carrier sensing in `t = 4.6` e determina che il canale non è vuoto dato che la trasmissione del pacchetto 9 è "percepita" da `3.8` a `4.8`.
- Quindi non viene trasmesso, dato che il canale non è vuoto.

**Risultato Finale:***
- Pacchetti non spediti: `2, 3, 6, 6, 8, 10, 11`.
- Pacchetti spediti con successo: `1, 9`.
- Nodi spediti ma che hanno avuto una collisione: `4, 5`.
