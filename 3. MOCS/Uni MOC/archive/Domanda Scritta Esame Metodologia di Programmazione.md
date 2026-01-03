---
created: 2024-06-20T18:32
updated: 2024-06-20T22:17
---

## MVC (Model View Controller)

MVC è l'acronimo per il design pattern chiamato Model View Controller, che come tutti i design pattern si occupa di risolvere un problema comune nell'ambiente della programmazione. 

I design pattern architetturali definiscono la struttura generale del codice, suddividendola in diverse componenti e stabilendo le modalità di interazione tra di essi. Questo è necessario per separazione delle responsabilità all'interno di un'applicazione e per ridurre avere maggiore controllo sulle dipendenze interne del codice.

Avere controllo su queste caratteristiche ci permette di:
- Mantenere il programma più facilmente.
- Riutilizzare alcune componenti del codice, in altre applicazioni e circostanze (modularità).
- Isolare le singole strutture, per testare e scovare eventuali errori più efficientemente.

In particolare l'obbiettivo dell'MVC è suddividere la struttura del codice in tre componenti principali:
- `Model`
- `View`
- `Controller`

### Model

Il `Model` può essere vista come la parte centrale dell'architettura, qui si trova quella parte del codice che si occupa di accedere al database e ai dati contenuti da esso, elaborarli e fornirli al componente `View`, per poi essere visualizzati dall'utente.

Una delle caratteristiche principali del `Model` è che non può avere dipendenze al di fuori del suo stesso package, questo significa che non può utilizzare risorse (codice, asset ...) contenute in `View`, `Controller`, o qualsiasi altro componente del programma. 

Questa caratteristica permette al `Model` di raggiungere un livello di indipendenza totale, garantendo la una massima riusabilità in diversi contesti e applicazioni.

In contesto pratico, questo significa che il diagramma UML di un software che implementa MVC sarà caratterizzato dal fatto che dal package `Model` partiranno frecce unidirezionali dirette verso il package `View` e al package Controller, indicando che il `Model` non dipende direttamente da queste componenti, ma che quest'ultimi dipendono dal `Model`.


### View 

Il modulo `View` può essere considerato come la parte dell'architettura che si occupa della visualizzazione dei dati e dell'interfaccia con l'utente.

Questo modulo a due compiti principali: 
1. Creazione dell'interfaccia: Il `View` riceve i dati dal `Model`e si occupa di visualizzarli su un interfaccia ,  
2. Ricezione dei dati in Input: Quando l'utente interagisce con l'interfaccia utente, il modulo `View` cattura tali interazioni e le inoltra al `Controller` per l'elaborazione.


Questo significa che il diagramma UML di un software che implementa MVC sarà caratterizzato dal fatto che:
- Dal package `View` partirà una freccia unidirezionale diretta verso il package `Controller` (indicando che `Controller` dipende da `View` e non vice versa) 
- Il package `View` riceverà una freccia unidirezionale partita dal package `Module` (indicando che `View` dipende da `Module`)


### Controller

Il `Controller` è quella parte dell'architettura che si pone come intermediario tra `Model` e `view`, In particolare:
1. Riceve input le azioni utente captate dal modulo `View`.
2. Elabora le informazioni ricevute: Il `Controller` è responsabile di interpretarle e decidere come gestirle le informazioni ricevute. 
3. Aggiorna il modulo `Model` in base all'elaborazione degli input.
    - Dopo aver elaborato le informazioni ricevute dall'utente, il `Controller` interagisce con il `Model` per aggiornare i dati in base alle azioni dell'utente. Questo potrebbe significare aggiornare i dati nel database, eseguire calcoli o qualsiasi altra operazione.

---
## Observer Observable

Con Observer Observable si indica un design patter di tipo comportamentale, ovvero un tipo di patter che ha l'obbiettivo di migliorare la comunicazione e l'assegnazione dei compiti tra gli oggetti all'interno dell'architettura.

In questo pattern ci sono due ruoli principali l'`Observer` e l'`Observable` 
- Gli `Observer` sono gli oggetti che devono essere informati dei cambiamenti di stato.
- L'`Observable` che si occupa di informare gli oggetti `Observer` di un eventuale il cambiamento di stato, consentendo loro di aggiornarsi di conseguenza. 

### MVC implementata con il supporto di Observer Observable

Implementare l'MVC con il supporto di Observer Observable ci aiuterà a ridurre ancora di più le varie dipendenze tra `Model`, `view` e `Controller`, in particolare a ridurre la dipendenza diretta di `Model` da `Controller`.

##### Implementazione
Ci sono più modi per implementare il pattern Observer-Observable e la scelta dipende dalle esigenze specifiche del progetto.

Potremmo utilizzare il patter Observer Observable per rappresentare la comunicazione tra `Model` e `View` facendo implementare a `Model` l'interfaccia  `Observable` e a `View` l'interfaccia `Observer` in modo tale da far comunicare i cambiamenti da Model a View.

Facendo ciò però non risovverremo una delle criticità principali ovvero la dipendenza che `Model` ha di `Controller`.
Per risolvere questa criticità possiamo far implementare a `Controller` l'interfaccia `Observable` e a `Model` l'interfaccia `Observer` in modo tale che quando il `Controller` riceve input dall'utente, può aggiornare il `Model` attraverso il pattern Observer-Observable, eliminando così la dipendenza diretta tra `Model` e `Controller`,  rendendo model veramente indipendente da tutti i componenti dell'architettura MVC.


