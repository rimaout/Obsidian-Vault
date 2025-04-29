---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-04-28T10:26
updated: 2025-04-28T12:43
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
	2.  Due categorie di post *Asta* o *Acquista Subito*:
		- *Asta* prevede:
			- Prezzo iniziale (Reale positivo)
			- Rialzo (Reale Positivo)
			- Prezzo corrente (Reale positivo, ogni volta che viene fatto un rialzo il prezzo corrente + rialzo, il prezzo corrente, inizialmente, è uguale al prezzo iniziale)
			- Scadenza (Data e Ora)
			- Alla fine della scadenza dell' asta dobbiamo salvare.
				- Bid vincitore (se esiste) (v.r. 5)
		- *Acquista Subito* prevede:
			-  Prezzo (Reale positivo)

3. Requisiti **Oggetti**:
	- 1. Descrizione (Stringa)
	- 2. Categoria Oggetto (è una sotto categoria v.r. 4)
	- 4. Metodo di pagamento accettato (bonifico e/o carta di credito)
	- 5. Gli oggetti possono essere *nuovi* o *usati*
		- Un oggetto *nuovo* prevede:
			- Anni di Garanzia (>= 2)
		- Un oggetto *usato* prevede:
			- Anni di Garanzia (>= 0)
			- Stato (ottimo, buono, discreto, da sistemare)

4. Requisiti **Categoria**: 
	- Nome (Stringa)
	- Una categoria può essere anche di secondo livello, in questo caso avrà un informazione aggiuntiva:
		- sotto categoria (Categoria)

5. Requisiti **Bid**:
	- Post (v.r. 2)
	- Bidder (Utente v.r. 1)
	- Istante (Data e Ora)
	- Offerta (Reale positivo ed è uguale al prezzo corrente del post + Rialzo)

6. Requisiti **Feedback**:
   - Acquirente (Privato v.r. 4)
   - Venditore (Utente)
   - voto (intero da 0 a 5)
   - commento (stringa opzionale)


