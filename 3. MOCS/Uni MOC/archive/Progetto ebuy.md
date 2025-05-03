---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-04-28T10:26
updated: 2025-05-02T13:24
---
1. Requisiti **Utente**:
	- 1. Nome (Stringa)
	- 2. Data Registrazione (Data)
	- 3. Post publicati (v.r. 2)
	- 4. Esistono due categorie di utenti *privati* e *professionali*:
		- Gli utenti professionali prevedono:
			- URL_vetrina (Stringa)
			- Popolarità (bassa, media, alta)

>[!note] Operazioni Utente
>
>Utenti professionali possono fare solo vendite, gli utenti privati possono fare sia vendite che compere.
>	
>Operazioni Utente: 
>- publica post (asta o acquista subito)
>- Acquista oggetto (solo per posto acquista subito, dopo un acquisto viene ricalcolata la popolarità del venditore se professionale)
>- fai offerta (bid)
>- fai feedback (dopo un feedback deve essere ricalcolata l'affidabilità del venditore(professionale e non))

2. Requisiti **Post**:
	1. Oggetto in vendita (v.r. 3)
	2. Metodo di pagamento accettato (bonifico, carta di credito, ecc) (oss: ecc indica che dovrà essere estendibile)
	3. Istante di pubblicazione (data e ora)
	4. Due categorie di post *Asta* o *Acquista Subito*:
		- *Asta* prevede:
			- Prezzo iniziale (Reale positivo)
			- Rialzo (Reale Positivo)
			- Prezzo corrente (Reale positivo, ogni volta che viene fatto un rialzo il prezzo corrente + rialzo, il prezzo corrente, inizialmente, è uguale al prezzo iniziale)
			- Scadenza (Data e Ora > Istante istante di pubblicazione)
			- Alla fine della scadenza dell' asta dobbiamo salvare.
				- Bid vincitore (se esiste) (v.r. 5)
		- *Acquista Subito* prevede:
			-  Prezzo (Reale positivo)

3. Requisiti **Oggetti**:
	- 1. Descrizione (Stringa)
	- 2. Categoria Oggetto (è una sotto categoria v.r. 4)
	- 3. Gli oggetti possono essere *nuovi* o *usati*
		- Un oggetto *nuovo* prevede:
			- Anni di Garanzia (intero >= 2)
		- Un oggetto *usato* prevede:
			- Anni di Garanzia (intero >= 0)
			- Stato (ottimo, buono, discreto, da sistemare)

4. Requisiti **Categoria**: 
	- Nome (Stringa)
	- Una categoria può essere anche di secondo livello, in questo caso avrà un informazione aggiuntiva:
		- sotto categoria (Categoria)

5. Requisiti **Bid**:
	- Asta (v.r. 2)
	- Bidder (Utente v.r. 1)
	- Istante (scadenza asta > Data e Ora > istante di pubblicazione del post)
	- Offerta (Reale positivo ed è uguale al prezzo corrente del post + Rialzo)
	- Il prezzo finale di vendita è calcolabile ed pari a prezzo iniziale + num_rialzi * valore_rialzi
	- Non possono essere piazzati due bid nello stesso istante per la stessa asta

***oss:*** in UML non è possibile direttamente vincolare il fatto che un istante deve essere maggiore di un altro, per fare ciò quindi dobbiamo creare un sistema che renda impossibile creare un bid con istante di offerta precedente ad un istante di pubblicazione

6. Requisiti **Feedback**:
   - Acquirente (Privato v.r. 1.4)
   - Venditore (Utente)
   - voto (intero da 0 a 5)
   - commento (stringa opzionale)


>[!note] Specifica della classe Asta
>
>----- Operazioni di classe -----
>```
>fine(): DataOra
>	precondizioni: nessuna
>	postcondizioni:
>		- non
>```


>[!note] Specifica della classe Bid
>
>----- Vincoli Esterni -----
>
>```
>[V.Bid.istante_dopo_publicazione_asta]
>
>Per ogni b:Bid, sia a:postOggettoAsta tale che esista il link b.istante >= a.instante_publicazione
>
>[V.Bid.istante_prima_di_scadenza_asta]
>
>Per ogni b:Bid, sia a:postOggettoAsta tale che esista il link (b, a):bid_asta, deve essere vero b.istante <= a.fine()
>
>[V.Bid.no_due_bid_stesso_istante_stessa_asta]
>```
