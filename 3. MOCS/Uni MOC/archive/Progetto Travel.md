---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-04-16T13:54
updated: 2025-04-16T14:50
---
## Specifica della classe Cliente

Ogni istanza di questa classe rappresenta un cliente.

============
Operazioni di classe:

	eta(d:Data): Intero >= 0
		pre: 
			d >= this.nascita
		post: 
			L'operazione non effettua side-effect sui dati.

			result =  (d - this.nascita) espressa in anni approssimata per difetto

## Specifica della classe Crociera

Un'istanza di questa classe rappresenta una crociera.


Operazioni di classe

fine(): Data

	- precondizioni: nessuna
	- postcondizioni:
		- non modifica il livello estensionale.

		- sia i il valore dell'attributo 'inizio' di 'this'.
		- sia it: Itinerario tale che esista il link 
		(this, it): croc_itin
		- sia d il risultato di it.durata_g()
		- result è i + d


posti_liberi(t: DataOra): Intero >= 0
	precondizioni:
		t <= adesso 
			e
		t <= this.inizio
			e
		deve esistere il link di associazione croc_nave
			che coinvolge 'this'

	post_condizioni:
		- Questa operazione non fa side-effect sui dati
		- il risultato 'result' è definito come segue:

		  - sia n: Nave tale che (this, n) è un link croc_nave
		  - sia c il valore dell'attributo capienza di n

		  - sia P l'insieme dei p: Prenotazione tali che
		  	(this, p) è un link pren_croc e p.istante <= t

		  - N = SUM     p.posti
		         p in P

		  - result = c - N

tocca(d: Destinazione, inizio: Data, fine: Data): Booleano
	precondizioni:
		inizio <= fine
			e
		se i periodi (this.inizio, this.fine()) e (inizio, fine) non sono disgiunti
	postcondizioni:
		- sia i: itinerario l'oggetto coinvolto nell'unico link `croc_uitin` con this `[(i, this,): croc_itin]`
		- se d non è in i.destinazione(), result è FALSE
		- altrimenti:
			- sia `i` il valore dell'attributo inizio fi this
			- se esiste i link (i, d):
				- partenza iniziale, se `inizio <= i <= fine`, result è `TRUE`.
			- altrimenti, se esiste i link (i,d): arrivo_finale, result è TRUE se inizio <= this.fine() <= fine
			- altrimenti, se esiste `ti: TappaIntermedia` tale che `(i, ti): intin_tappa` e `(ti, d): tappa_dest` e `(this.inizio + ti.arrivo.giorni, this.inizio + ti.ripartenza.giorni)` si sovrappone a `(inizio, fine)`, allora result è `TRUE` altrimenti è `FALSE`




======
Vincoli esterni

[V.Crociera.Prenotazione.no_overbooking]
Per ogni c: Crociera tale che esiste un link croc_nave che coinvolge c
	per ogni t: DataOra tale che t <= c.inizio

	deve essere vero che c.posti_liberi(t) >= 0

## Specifica della classe Destinazione

Un'istanza di questa classe rappresenta una destinazione, ossia un luogo toccato da itinerari di crociera.

Specifica delle operazioni di classe


esotica(): Booleano
	precondizioni: nessuna
	postcondizioni: 
		- nessuna modifica al livello estensionale.
		- il valore di ritorno 'result' è così definito:
			- Sia c:Continente tale che (this,c):dest_cont.
			result = true se e solo se c.esotico = True

## Specifica della classe Itinerario

Un'istanza di questa classe rappresenta un itinerario, cioè una sequenza ordinata di destinazioni, che può essere seguito dalle crociere.


**Specifica delle operazioni di classe**

durata_g(): Intero >= 0
	precondizioni: nessuna
	postcondizioni:
		- non modifica il livello estensionale.
		- il valore di ritorno result è così definito:
			- sia (this, d):arrivo_finale l'unico link arrivo_finale che coinvolge 'this'.
			- result è (this, d).ora.giorno


destinazioni(): Destinazione [1..*]
	precondizioni: nessuna

	postcondizioni:
		sia di: Destinazione l'oggetto tale che esiste il link
			(this, di): partenza_iniziale
		sia df: Destinazione l'oggetto tale che esiste il link
			(this, df): arrivo_finale

		sia Dt l'insieme degli oggetti d: Destinazione tale che 
			esista t:TappaIntermedia e (d, t):tappa_dest
			e (t, this):itin_tappa

		sia 'result' Dt Unione {di} Unione {df}


esotico(): Booleano
	precondizioni: nessuna
	postcondizioni:
		sia D = this.destinazioni()
		result è TRUE se e solo se esiste almeno un elemento d in D tale che 
		d.esotica() = TRUE

# Specifica dei tipi di dato

DeltaDataOra tipo record con i seguenti campi:
	- giorno: Intero > 0
	- ora: Ora

# Specifica delle operazioni dello Use-Case GestioneCompletaPrenotazioni


Operazioni

prenota(cl: Cliente, n_posti: Intero > 0, cr: Crociera): Prenotazione
	
	precondizioni: 
		adesso < cr.inizio
			e
		esiste il link dell'associazione croc_nave che coinvolge cr
			e
		cr.posti_liberi(adesso) >= n_posti

	postcondizioni:
		- il livello estensionale è modificato come segue:
			- viene creato l'oggetto p: Prenotazione con 
				p.istante = adesso e p.posti = n_posti
			- viene creato il link (p, cr): pren_croc
			- viene creato il link (p, cl): pren_cliente

		- il risultato 'result' è p

# Specifica dello use-case Statistiche

Operazioni

// Dato un periodo 'p', calcolare l'età media dei clienti che hanno prenotato, durante 'p', almeno una crociera che prevede una destinazione esotica (v. req. 3.5)

media_esotiche(inizio: Data, fine: Data): Reale >= 0
	precondizioni:
		inizio <= fine
			e
		esiste almeno un c: Crociera tale che
		- sia i: Itinerario tale che (cr, i): croc_itin
		- i.esotico() è TRUE
		e esiste un cl:Cliente e p: Prenotazione tale che
		(cl, p):pren_cliente e
		(p, cr):pren_croc
		e p.istante è tra inizio e fine

	postcondizioni:
		- sia C l'insieme dei cl:Cliente tale 
			esiste cr:Crociera e p: Prenotazione e i:Itinerario
			tali che 
				(cl, p):pren_cliente e
				(p, cr):pren_croc e
				(cr, i):croc_itin e
				e i.esotico()=TRUE
				e inizio <= p.istante <= fine

		- result è ( SUM c.eta(oggi) ) / |C| c in C

destinazioni_gettonate( inizio: Data, fine: Data): Reale 0..1
- **precondizioni:**
		inizio <= fine
			e
		// deve esistere almeno una destinazione toccata da almeno una crociera nel periodo in input
	esiste `d: Destinazione` e `c: Crociera` tale che `c.tocca(d, inizio, fine)`

- **postcondizioni:**
	- `{ 
			`(d, ncl, ncf) | D: Destinazione and ncl = |{c | c:LunaDiMiele and c.tocca(d, inizio, fine)}| 
				and
			`nfc = | {c | c:PerFamiglie and c.tocca(d, inizio, fine)} |`
		`}`
	- esiste `d`


