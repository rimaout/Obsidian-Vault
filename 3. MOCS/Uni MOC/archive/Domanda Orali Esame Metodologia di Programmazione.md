---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
completed: false
created: 2025-01-06T20:21
updated: 2026-01-31T13:32
---
# Domande che ha fatto il Faralli agli orali

## Risposte

**Mi parla delle classi interne?**
Il linguaggio Java consente di scrivere classi all'interno di altre classi, queste sono chiamate nested class o inner class a seconda del fatto che siano statiche oppure no.
Come tutti i membri di una classe, le classi interne possono essere dichiarate public, protected o private
(leggere anche ciò che ho scritto nella sezione static/non static perchè parlo delle classi interne)

**Perché esistono le classi annidate/interne?**
Per vari motivi:
- una classe può essere utile solo ad un'altra classe, quindi potrebbe essere logico tenere le due classi logicamente vicine
- Incrementare l'incapsulamento
- rendono il codice più leggibile e facile da mantenere

**C'è un principio al quale si fa riferimento con le classi annidate/interne?**
Risposta: _Incapsulamento_

Il principio di Incapsulamento è uno dei principi fondamentali della programmazione orientata agli oggetti e si basa sull'idea di nascondere i dettagli interni dell'implementazione e offrire un'interfaccia pubblica attraverso la quale gli utenti possono interagire con l'oggetto
Vantaggi:
- aiuta a migliorare la sicurezza del codice poichè evita accessi non autorizzati ai dati interni
- rende il software più robusto, strutturato e facile da mantenere
-  Incapsulando i dettagli complessi e presentando solo ciò che è necessario per l’uso, si riduce la complessità percepita e si facilita la comprensione del codice.

**Come deve essere una classe per non essere extendable da altre classi?**
Risposta: final

**Cos'è un parallel stream?**
Un _parallel stream_ in Java è una caratteristica introdotta con Java 8 che consente di suddividere automaticamente un’operazione su più thread.

Ci sono due tipi principali di Stream: stream sequenziale e stream parallelo.
Lo stream sequenziale esegue le operazioni sui dati nell'ordine in cui gli elementi appaiono nella sorgente (lista, array ecc) utilizzando un singolo thread.
Lo stream parallelo invece divide i dati in sottoinsiemi e assegna a ciascuno di essi un thread diverso, sfruttando il parallelismo, in questo modo le operazioni vengono eseguite simultaneamente.
In teoria, l’uso di un _parallel stream_ consente di accelerare le operazioni su grandi insiemi di dati, sfruttando la capacità dei processori multicore. Per esempio, se hai un’operazione che può essere divisa in parti indipendenti, un parallel stream permette che tali parti vengano eseguite in parallelo, riducendo il tempo di esecuzione complessivo.

Quindi riassumendo:
_Sequential stream_: Usa un solo thread, esegue le operazioni in ordine.
_Parallel stream_: Usa più thread, suddivide i dati e li elabora in parallelo.

Quando bisogna usare uno stream parallelo?
• Quando il problema è parallelizzabile
• Quando posso permettermi di usare più risorse (es. tutti i core del processore)
• La dimensione del problema è tale da giustificare il sovraccarico dovuto alla parallelizzazione

**Il parallelismo delle operazioni è sempre un vantaggio? In quali casi può provocare dei problemi?**
Il parallelismo delle operazioni NON è sempre un vantaggio, infatti in alcuni casi uno stream parallelo può risultare molto più lento di uno stream sequenziale.

In particolare usare un parallel stream non conviene nei seguenti casi:
- _Dati di piccole dimensioni_:  per un insieme di dati di piccole dimensioni, l’overhead di creare e gestire più thread può superare i benefici del parallelismo. L’inizializzazione dei thread, il coordinamento e la fusione dei risultati aggiungono un costo, che potrebbe non essere compensato dal guadagno in termini di prestazioni se i dati sono pochi.
- _Operazioni non indipendenti_: Il parallelismo funziona meglio con operazioni che possono essere eseguite indipendentemente. Se le operazioni hanno dipendenze tra loro, ciò può portare a risultati errati o richiedere un notevole sforzo per la sincronizzazione, riducendo i vantaggi del parallelismo.

In sintesi, il parallelismo non è sempre un vantaggio. Conviene quando si lavora su grandi insiemi di dati con operazioni indipendenti e su sistemi con molte risorse disponibili. In casi contrari, potrebbe causare più problemi di quanti ne risolva.

**Come funziona il meccanismo di cancellazione del tipo?**
L’algoritmo di cancellazione del tipo è l’algoritmo utilizzato dal compilatore Java per compilare i metodi e le classi generiche.
La cancellazione del tipo si verifica quando il compilatore traduce il metodo o la classe generica in bytecode Java.
In particolare segue questi passaggi:
1. Elimina la sezione del tipo parametrico e sostituisce il tipo parametrico con quello reale
2. Per default il tipo generico viene sostituito con il tipo Object (a meno di vincoli sul tipo, che possono essere espressi mediante le parole chiave extends e super)
Quindi in realtà vengono creati i metodi e le classi con il tipo concreto e non quelli con i generici.

**La trasformazione da tipo generico a Object può causare delle problematiche, quali?**
Poiché l’informazione sui tipi generici viene rimossa a tempo di compilazione, non è possibile verificare il tipo effettivo degli oggetti a runtime. Ad esempio, un’operazione come instanceof su un tipo generico darà un errore, perché il tipo non è più noto

**Come si fa ad evitare i suddetti comportamenti indesiderati nel principio di cancellazione del tipo? Principio PECS**
Risposto nella sezione sotto su Tipi generici e PECS

**Differenza tra una classe e un'interfaccia?**
Differenze fondamentali tra classi e interfacce:
- _Ereditarietà_: Una classe può estendere solo un’altra classe, mentre una classe può implementare più interfacce.
- _Metodi_: Le classi possono avere metodi concreti e astratti, mentre le interfacce (in Java 7 e precedenti) hanno solo metodi astratti. Da Java 8 in poi, le interfacce possono includere metodi concreti con l’uso di default o static.
- _Attributi_: Nelle classi, i campi possono essere di diversi tipi (pubblici, privati, ecc.), mentre nelle interfacce, i campi sono implicitamente public, static, e final.

**Che metodi possono esserci in un'interfaccia?**
Fino a Java 7 all'interno delle interfacce si potevano dichiarare solo metodi public e abstract
da Java 8 sono stati introdotti i metodi di default e i metodi statici
da Java 9 i metodi privati (di solito invocati all'interno di metodi di default)

**Da una versione di java in poi si possono avere metodi implementati, come sono questi metodi?**
Metodi di default, introdotti nelle interfacce a partire da Java 8 per permettere alle interfacce di fornire un implementazione senza rompere la compatibilità con il codice esistente.
Prima di Java 8, ogni metodo definito in un’interfaccia doveva essere astratto e implementato da tutte le classi che la implementavano. Con i metodi di default, un’interfaccia può fornire un comportamento di base, che le classi possono usare senza dover necessariamente ridefinirlo.
Le classi che implementano un’interfaccia possono scegliere di overrideare (sovrascrivere) i metodi di default, ma non sono obbligate a farlo.

esempio di dichiarazione di un metodo di default
```Java
interface Animale {
    void mangia();

    // Metodo di default
    default void dormi() {
        System.out.println("L'animale sta dormendo.");
    }
}
```

**Hashcode e equals**
I metodi `equals()` ed `hashCode()` sono metodi particolari di java che ogni oggetto eredita dalla classe `java.lang.Object`
Il metodo equals per vedere se due oggetti sono uguali vede se si riferiscono alla stessa area di memoria.
Il metodo hashCode() restituisce un numero intero (hash code) che rappresenta l’oggetto.
Questo è particolarmente utile nelle strutture di dati come HashMap e HashSet, che usano l’hash code per organizzare gli oggetti. Se due oggetti sono considerati uguali secondo il metodo `equals()` hanno lo stesso hashcode, tuttavia se due oggetti hanno lo stesso hashcode non necessariamente devono essere uguali secondo il metodo `equals()`

se il metodo equals viene ridefinito deve esserlo anche il metodo hashcode per non violare il contratto.

**Qual'è la differenza tra iterable e iterator?**
risposta nella sezione iterable e iterator sotto

**Descrivere la gerarchia degli iterable**
Risposto sotto nella sezione Collection

**Svantaggi degli stream**
Gli stream non sono riutilizzabili. Una volta consumato uno stream (ad esempio con un’operazione terminale come collect(), non può essere riutilizzato. Se vuoi eseguire un’altra operazione, devi crearne uno nuovo.

**Quali sono le strutture dati che mantengono l'ordine? (di inserimento)**
ArrayList, LinkedList, LinkedHashSet, LinkedHashMap, TreeSet

**uso di ::**
In Java, l’operatore :: è chiamato **operatore di riferimento a metodo** (**method reference**). È una funzionalità introdotta in **Java 8** che permette di fare riferimento a metodi o costruttori senza invocarli direttamente. I riferimenti ai metodi sono spesso usati in combinazione con le **espressioni lambda** per rendere il codice più conciso e leggibile.

esistono 4 principali utilizzi di questo operatore:
- riferimento a metodo statico
- riferimento a metodo di istanza su un oggetto particolare
- riferimento a metodo di istanza su oggetti arbitrari di un tipo particolare
- riferimento a costruttore

**flatMap**
l metodo flatMap in Java è una delle operazioni più potenti e versatili disponibili nei **stream** (introdotti in **Java 8**). Viene utilizzato per trasformare e “appiattire” i risultati delle operazioni di mappatura, evitando di avere uno stream di strutture annidate (come una lista di liste) e restituendo invece uno **stream piatto** di elementi.
In altre parole, combina tutti i singoli stream (o strutture) risultanti in uno **stream unico** (piatto).

**heap stack e metaspace**
In Java, la memoria viene gestita principalmente in tre aree principali: **Heap**, **Stack**, e **Metaspace**. Ciascuna di queste ha un ruolo specifico nella gestione degli oggetti, delle variabili e dei metadati del programma. Ecco una breve spiegazione di ciascuna:

- Heap: area di memoria più grande usata per allocare oggetti e variabili durante l'esecuzione del programma, tutti gli oggetti e le istanze delle classi sono allocati qui.
- Stack:  Lo stack è una porzione di memoria più piccola e più veloce, utilizzata per gestire le variabili **locali**, i **puntatori ai metodi** e le **chiamate ai metodi**.
- Metaspace: Per memorizzare i metadati delle classi e altre informazioni di runtime.

**enum**
Le enumerazioni sono un tipo java che definisce un elenco di costanti enumerative, implicitamente static. Non è possibile creare un oggetto di tipo enum.
Le enum sono di fatto delle classi particolari e in quanto tali possono contenere oltre alle costanti enumerative: costruttori, campi e metodi.
Il metodo statico values(), che possiede ogni enumerazione, restituisce un array delle costanti enumerative.

**come implementare hashcode?**
Hashcode è un metodo di Object che consente di associare ad ogni oggetto un codice hash (ovvero un numero intero) che sarà lo stesso per due oggetti uguali.

1. **Numeri primi**: Si scelgono due numeri primi, uno per inizializzare il codice hash e l’altro per moltiplicare i valori dei campi dell’oggetto. I numeri primi vengono scelti perché migliorano la distribuzione dei valori hash, riducendo le collisioni (cioè quando due oggetti diversi hanno lo stesso hashcode).
2. **Hash di ogni campo**:
• Per i campi **primitivi** (es. int, double), viene utilizzato direttamente il loro valore.
• Per gli oggetti, viene chiamato hashCode() su ciascun campo per ottenere il loro codice hash.
3. **Somma e moltiplicazione**:
• Si inizia con un valore iniziale per l’hash (di solito un numero primo come **31**).
• Per ogni campo dell’oggetto, il valore corrente del codice hash viene **moltiplicato** per un numero primo (come 31) e poi si **somma** l’hash o il valore del campo al risultato.

• Questo processo di **moltiplicazione** e **somma** viene ripetuto per tutti i campi.

- altra domanda:
Sì, in Java un’interfaccia può **estendere un’altra interfaccia**. In questo caso, l’interfaccia derivata eredita tutti i metodi dell’interfaccia “genitore” (o interfacce genitrici, nel caso di ereditarietà multipla), anche se questi non sono implementati. Le classi che implementano l’interfaccia derivata devono fornire implementazioni per tutti i metodi ereditati, a meno che non si tratti di **interfacce funzionali** (con un solo metodo astratto).

## Da Rispondere
Mancanti 5 (rispondere finito il ripasso per prova)

**Cos'è il binding e cos'è il binding dinamico e la loro differenza?**

**Vantaggi e svantaggi dell'uso di stream?**

**Mi spiega la questione della parallelizzazione negli stream e dell'impatto delle operazioni stateful e stateless?**

**Cosa sono i tipi generici e come vengono gestiti?**
Prima parte della domanda risposta nella parte sotto sui tipi generici, da capire la seconda

**Perché l'implementazione dei tipi generici in Java è limitata? Parliamo dell'algoritmo di cancellazione del tipo? Perché si chiama così e come funziona? Esempio array di mela, pera, frutta? Principio PECS cosa dice? (Lode)**
## Cose esplorate autonomamente
- **Differenza tra static e non static nelle classi, metodi e campi**
Risposta:
In Java possono essere dichiarate static le classi, i metodi e i campi.
_Classi_
Le uniche classi che possono essere dichiarate static sono quelle interne
Static Nested Class --> classe interna statica
Inner Class --> classe interna non statica

Una Nested Class può essere istanziata senza istanziare la sua classe esterna, non ha accesso ai membri di istanza della classe esterna, ma può accedere ai suoi membri statici (campi e metodi statici)
Una Inner Class invece non può essere istanziata senza creare un'istanza della classe esterna, ha accesso ai membri di istanza della classe

L'utilità delle classi interne è quella di migliorare l'organizzazione del codice e nascondere i dettagli di implementazione, una nested class è migliore per incapsulare funzionalità che non dipendono dall'istanza della classe esterna, mentre le inner class per incapsulare funzionalità che richiedono l'accesso all'istanza della classe esterna

_Metodi_
I metodi statici appartengono alla classe e non a qualsiasi istanza della classe, questo implica che possono essere invocati utilizzando direttamente il nome della classe senza crearne un'istanza, i metodi non statici solo tramite l'istanza delle classe.
Possono chiamare solo altri metodi statici e devono utilizzare solo campi statici, i metodi di istanza invece possono accedere a tutti i membri della classe (sia statici che di istanza)
Non hanno accesso ai membri di istanza della classe, ma hanno accesso ai campi di classe.
Sono spesso utilizzati per utilità generali, factory methods, o per operazioni che devono essere condivise tra tutte le istanze.

_Campi_
I campi statici appartengono alla classe piuttosto che alla singola istanza della classe, quindi ciò significa che c'è una sola copia di un campo statico condivisa tra tutte le istanze della classe.
Possono essere accessibili direttamente tramite il nome della classe senza la necessità di un'istanza.
Sono utili per valori o stati che devono essere condivisi tra tutte le istanze della classe ad esempio una costante o un contatore

I campi static vengono allocati nel MetaSpace

- **Differenza tra final e non final in classi, metodi e campi**
_Classi_
Una classe che viene dichiarata final non può essere estesa.
Ciò implica che nessuna classe può ereditare da una classe final, è utile per impedire che la classe venga modificata attraverso l'ereditarietà.

_Metodi_
un metodo dichiarato come final non può essere sovrascritto da nessuna sottoclasse, è utile quando si vuole garantire che non venga alterato nelle sottoclassi

_Campi_
Un campo che viene dichiarato final non può essere modificato una volta assegnato.
Deve essere inizializzato al momento della dichiarazione o nel costruttore della classe

- **Modificatori public, protected e private**
_Classi_
Una classe private può essere vista solo all'interno della classe in cui è dichiarato
In Java solo le classi interne possono essere dichiarate con i modificatori private e protected.
Una classe interna private è accessibile solo all'interno della classe che la contiene, mentre una classe interna protected è accessibile sia all'interno della classe che la contiene che dalle sottoclassi e dalle classi dello stesso package.
Le classi principali possono essere o public (classe accessibile da qualsiasi altra classe in qualsiasi package) o con visibilità di package (che significa che la classe è accessibile solo dalle altre classi nello stesso package)

_Metodi e Campi_
possono essere dichiarati come `private`, `public`, `protected`
private --> il membro è visibile solo all'interno della classe
public --> il membro è visibile da qualsiasi altra classe in qualsiasi pacchetto
protected --> il membro è accessibile all'interno della stessa classe, dalle sottoclassi (anche in pacchetti diversi) e dalle altre classi nello stesso pacchetto

Se non viene specificato il modificatore (se è public, private o protected) il membro è accessibile solo dalle altre classi nello stesso pacchetto

- **Differenza tra abstract e non abstract**
possono essere definiti abstract le classi e i metodi.
_Classi_
Una classe abstract, a differenza di una non abstract, non può essere istanziata direttamente, ma solo attraverso una sottoclasse che la estende.
Una classe astratta può contenere sia metodi astratti che non, mentre quelle non abstract possono contenere solo metodi non abstract

_Metodi_
Un metodo dichiarato come abstract non fornisce un'implementazione, deve essere implementato dalle sottoclassi della classe astratta che lo contiene.
Un metodo non abstract invece deve necessariamente fornire un'implementazione.
Una sottoclasse di una classe astratta che contiene metodi astratti deve fornire un'implementazione per tutti i metodi astratti della superclasse.

- **Polimorfismo in Java**
Il Polimorfismo è un principio della programmazione orientata agli oggetti che consente a un oggetto o un metodo di comportarsi in modi diversi a seconda del contesto.
In Java esistono due diversi tipi di polimorfismo e si differenziano principalmente per il modo e il tempo in cui viene deciso quale metodo invocare.
_Polimorfismo statico_: viene eseguito durante la fase di compilazione (prima del runtime) e il suo uso si riflette principalmente nell'overloading dei metodi, che consiste nel fornire, all'interno della stessa classe, diverse implementazioni di un metodo con lo stesso nome, ma che accettano diversi tipi di dati o numero di argomenti. Anche il tipo di ritorno può essere diverso ma non è sufficiente da solo per distinguere i metodi. Il metodo invocato è scelto in base al tipo, numero e ordine dei parametri.
_Polimorfismo dinamico_: si verifica durante l’esecuzione e viene implementato attraverso l’ereditarietà e l’override dei metodi. Questo avviene quando una sottoclasse fornisce una sua versione (override) di un metodo definito nella sua superclasse. Il metodo appropriato viene scelto in base al tipo effettivo dell’oggetto a runtime.

I vantaggi del polimorfismo sono quelli di aggiungere nuove funzionalità modificando al minimo il codice e permettere scrivere codice molto più riutilizzabile

- **Tipi generici**
I tipi generici in Java sono un potente meccanismo che permette di scrivere codice flessibile e riutilizzabile mantenendo al tempo stesso la sicurezza del tipo (type safety). Ciò consente di creare classi, interfacce e metodi che operano su tipi di dati specificati solo al momento dell’uso. Ad esempio, una classe può essere scritta per gestire una lista di oggetti senza dover specificare in anticipo di che tipo sono questi oggetti, il che elimina la necessità di fare cast espliciti e minimizza gli errori di runtime.

```Java
public class Box<T> {
    private T item;

    public void set(T item) {
        this.item = item;
    }

    public T get() {
        return item;
    }
}
```

Per convenzione i tipi generici sono chiamati con le lettere T, S (E nel caso degli elementi di una collection)
Non è possibile utilizzare i tipi primitivi con tipi generici come int, double e char, questo perchè durante la cancellazione del tipo, il tipo generico viene sostituito con Object, ma se provassi a usare un tipo primitivo con un generico, il compilatore non saprebbe come tradurlo, dato che i tipi primitivi non possono essere trattati come oggetti.

Non è permesso l'upcasting tra i tipi generici (upcasting in Java è il processo di conversione di un oggetto da un tipo più specifico (come una sottoclasse) a un tipo più generico (come una superclasse o un’interfaccia)

_Esempio dell'ArrayList di Mele con dentro una Pera
```Java
public class ViolenzaSuUnArrayList {
    public static void main(String[] args) {
        ArrayList<Mela> mele = new ArrayList<Mela>();

        prendiFrutta(mele);

        // qui avrei una lista di mele con una pera!!!
        System.out.println(mele.toString());
    }

    public static void prendiFrutta(ArrayList<Frutto> frutti) {
        frutti.add(new Pera());
    }
}
```
- C'è una lista di Mele, che contiene oggetti di tipo Mela
- si chiama il metodo `prendiFrutta` passando in input la lista di mele
- il metodo `prendiFrutta` accetta una lista di frutti e cerca di aggiungere una pera a questa lista

Tuttavia come detto in precedenza non è possibile passare da `ArrayList<Mela>` a `ArrayList<Frutto>`, se fosse possibile si avrebbe una lista di mele con dentro una pera

L'upcasting è permesso a tempo di compilazione, al contrario delle collection, ma otteniamo un'errore se violiamo il contratto

Soluzione
```Java
public static void prendiFrutta(ArrayList<? super Frutto> frutti) {
    frutti.add(new Pera());
}
```

_Le interfacce Comparable e Comparator sono generiche)_
 l’interfaccia `Comparable<T>` che definisce un ordinamento naturale sul tipo grazie al metodo `compareTo(T o)` che confronta l'oggetto corrente (`this`) con l'oggetto passato come argomento (`o`) . È definito all'interno della stessa classe
 ritorna:
 - 0: sono uguali
- -1: se <
- +1: se >

L’interfaccia `Comparator<T>` è utilizzata quando vuoi fornire un criterio di ordinamento esterno alla classe. A differenza di Comparable, che viene implementata all’interno della classe, un Comparator viene definito in una classe separata e può essere utilizzato per specificare molteplici modi di confrontare oggetti.
metodo `compare(T o1, T o2)`
Questo metodo confronta due oggetti (o1 e o2).
stessa logica di ritorno di compareTo

espone 2 metodi: compare ed equals. In questo caso notevole il metodo equals, che dovrebbe essere astratto in base alle regole delle interfacce, in realtà eredita l’implementazione di equals definita in Object.

L'uso principale dei tipi generici è nelle collezioni

Parole chiave _extends_ e _super_ nei tipi generici.
- extends: T deve essere un sottotipo della classe specificata o la classe stessa (covarianza)
- super: T deve essere una superclasse della classe specificata o la classe stessa (controvarianza)

- **PECS**
Il principio PECS regola l'uso delle wildcards (o jolly) `?`, questo principio viene applicato quando si lavora con collezioni generiche.

Nel caso in cui non sia necessario utilizzare il tipo generico T nel corpo della classe o del metodo, è possibile utilizzare il jolly ?
`extends` e `super` esistono principalmente per scrivere o leggere su/da una collezione generica
_Producer extends, Consumer supers_

- si usa `extends` quando hai bisogno di leggere o prelevare dati da una collezione, ma non aggiungere nuovi dati alla collezione, in questo caso la collezione diventa una fonte di dati quindi un "Producer", quindi se si ha una collezione che produce oggetti di un certo tipo si dovrà usare `? extends Tipo`. Questo consente di accettare sottoclassi di quel tipo. Un esempio pratico potrebbe essere una lista che fornisce numeri da utilizzare in un calcolo

```Java
public void stampaNumeri(List<? extends Number> numeri) {
    for (Number num : numeri) {
        System.out.println(num);
    }
}
```

- si usa `super` quando hai bisogno di aggiungere dati a una nuova collezione, quindi la collezione viene detta "Consumer", bisognerà scrivere `? super Tipo`. Questo permette alla collezione di accettare oggetti di quel tipo o di una sua superclasse. Per esempio, puoi aggiungere numeri a una lista che può accettare interi o qualsiasi tipo superiore a Integer, come Number o Object.

```Java
public void aggiungiNumeri(List<? super Integer> lista) {
    lista.add(10);  // Aggiungo un Integer alla lista
}
```

Quindi, **produrre dati** significa ottenere elementi da una collezione (come leggere una lista), mentre **consumare dati** significa fornire nuovi elementi a una collezione (come aggiungere dati a una lista).

- **Interfacce**
Le interfacce sono uno strumento che Java mette a disposizione per consentire a più classi di fornire e implementare un insieme di metodi comuni. L'implementazione dei metodi rimane non definita.
Nella loro versione originale le interfacce contenevano solo metodi astratti, la cui implementazione era delegata alle classi che implementano l'interfaccia.
Java 8 e Java 9 hanno introdotto sostanziali aggiunte a quello che può essere definito al loro interno.
Oggi un’interfaccia può contenere:
- Costanti.
- Metodi astratti
- Metodi con implementazione di default
- Metodi statici
- Metodi privati utilizzati nei metodi di default

I campi definiti all’interno di un’interfaccia sono implicitamente public, static e final.
I metodi definiti all’interno di un’interfaccia sono implicitamente public e abstract.

dichiarazione di un'interfaccia 
```Java
public interface SupportoRiscrivibile
{
	int TIMES = 1000;

	void leggi();
	void scrivi();
}
```

Le interfacce risolvono il problema dell’ereditarietà multipla, infatti in Java è possibile estendere una sola classe mentre è possibile implementare un numero qualsiasi di interfacce, le due cose possono avvenire contemporaneamente.

Implementando un'interfaccia una classe deve implementare tutti i metodi specificati dall'interfaccia o la classe deve essere dichiarata abstract.

Nel momento in cui una classe C decide di implementare un’interfaccia I, tra queste due classi si instaura una relazione di tipo is-a, ovvero C è di tipo I
• Comportamento simile a quello dell’ereditarietà
• Quindi anche per le interfacce valgono le regole del polimorfismo

- **Interfaccia SAM e differenza con le interfacce funzionali**
Un’interfaccia SAM, anche detta Single Abstract Method, è un’interfaccia che espone un singolo metodo astratto. A ogni metodo che accetta una SAM si può passare una lambda compatibile.

Ciò che contraddistingue un'interfaccia funzionale da una SAM è che un'interfaccia funzionale ha un solo metodo astratto ma ne può contenere anche altri non astratti mentre una SAM ha un unico metodo che per di più deve essere astratto.

- **Iterable e Iterator**
Sono due interfacce standard di java che disaccopiano l'oggetto su cui iterare dall'oggetto che tiene la posizione di iterazione

Interfaccia `java.util.Iterator<E>`
È un interfaccia che permette di iterare su collezioni, questa espone tre metodi `hasNext()`, `next()` e `remove()`
E’ in relazione con l’interfaccia Iterable nel senso che il metodo `iterator()` dell'interfaccia Iterable restituisce un iterator

La classe su cui devo iterare implementa Iterable e non Iterator

differenze tra i due:
• Iterable è responsabile di fornire un iteratore per una collezione, tramite il metodo iterator().
• Iterator è responsabile del processo di iterazione effettiva, controllando se ci sono più elementi e fornendo il successivo.

• Iterable definisce una collezione che può essere iterata.
• Iterator fornisce un meccanismo per accedere in modo sequenziale agli elementi di una collezione.

• Solo le collezioni che implementano Iterable possono essere iterate direttamente tramite un ciclo for-each.
• L’uso di Iterator richiede un ciclo while o un controllo esplicito dei metodi hasNext() e next().

Quindi, in sostanza, Iterable è l’interfaccia che abilita il comportamento iterabile di una collezione, mentre Iterator gestisce il ciclo e l’accesso agli elementi stessi.

- **il metodo clone e la differenza tra shallow copy e deep copy**
Per creare una copia di un oggetto è necessario richiamare `clone()`

Tuttavia l’implementazione nativa di default di `Object.clone` copia l’oggetto campo per campo (shallow copy)
- Ottimo se i campi sono tutti primitivi
- Problematico se i campi sono riferimenti

Se il nostro oggetto contiene riferimenti e vogliamo evitare che la copia contenga un riferimento allo stesso oggetto membro, non possiamo chiamare semplicemente (o non chiamiamo proprio) `super.clone()`

E' necessario implementare l'interfaccia "segnaposto" `Cloneable` altrimenti `Object.clone` emetterà semplicemente l'eccezione `CloneNotSupportedException`

Per evitare la copia dei riferimenti, è necessaria la clonazione "profonda" (deep cloning)
– Si può usare `Object.clone` per la clonazione dei tipi primitivi
– E richiamare manualmente `.clone()` su tutti i campi che sono riferimenti ad altri oggetti, impostando i nuovi riferimenti nell'oggetto clonato

- **Classi anonime**
È possibile definire classi anonime (senza nome) che implementano un'interfaccia o estendono una classe.
Vengono usate principalmente per creare istanze di classi o implementazioni di interfacce, senza la necessità di definire una nuova classe separata. Sono particolarmente utili quando hai bisogno di fornire un’implementazione personalizzata di una classe o interfaccia e tale implementazione è usata solo in un punto specifico del codice.
Non possono essere riutilizzate o istanziate di nuovo da un’altra parte del codice.

sintassi 
```Java
new SuperClasse() {
    // Override metodi o aggiungi nuovi comportamenti
};

// oppure

new NomeInterfaccia() {
    // Implementa metodi dell'interfaccia
};
```

Utili in determinati contesti (ad esempio, per creare un iteratore al volo)

- **Espressioni lambda**
Le espressioni lambda in Java sono una caratteristica introdotta con Java 8 che consente di scrivere codice in modo più compatto, soprattutto quando si lavora con interfacce funzionali.
Tali espressioni creano oggetti anonimi assegnabili a riferimenti a interfacce funzionali compatibili con l’intestazione (input/output) della funzione creata

Un’espressione lambda rappresenta un’implementazione concisa di un metodo astratto di un’interfaccia funzionale (un’interfaccia con un solo metodo astratto). Le lambda rendono il codice più compatto e leggibile.

sintassi
```Java
(int a, int b) -> { return a+b; }
// si può scrivere anche come
(a, b) -> a+b;
```

- Il tipo dei parametri in input è opzionale, perché desunto dal contesto (a quale interfaccia funzionale facciamo riferimento?)
- Le parentesi tonde sono opzionali se in input abbiamo un solo parametro
- Le parentesi graffe intorno al codice della funzione sono opzionali se è costituito da una sola riga

E' da consigliare l'impiego delle espressioni lambda principalmente quando il codice si scrive su una sola riga

- **Stream**
Interfaccia `java.util.stream.Stream`
 Gli stream rappresentano una sequenza di elementi provenienti da una sorgente (come collezioni o array) e permettono di eseguire una o più operazioni su di essi. Al contrario delle Collection, uno Stream non memorizza né modifica i dati della sorgente, ma opera su di essi

Le operazioni eseguite in uno stream possono essere:
- _intermedie_: restituiscono un altro stream su cui continuare a lavorare, ad esempio `map()`, `filter()`, `sorted()`
- _terminali_: restituiscono il tipo atteso, ad esempio `collect()`, `count()`

una volta che si è effettuata un'operazione terminale su uno stream esso non può più essere riutilizzato.
Gli stream vengono usati all'interno del Builder Pattern.

Le operazioni su uno stream sono eseguite in modo “pigro”, cioè vengono elaborate solo quando una operazione terminale è invocata. Questo approccio consente di ottimizzare le prestazioni, evitando di processare tutti gli elementi inutilmente, questo comportamento è detto **lazy behavior**

Le operazioni inoltre possono essere:
- _stateless_: l'elaborazione dei vari elementi può procedere in modo indipendente (es. filter), il compilatore decide l'ordine più efficiente da seguire per l'esecuzione del programma
- _stateful_: l'elaborazione di un elemento potrebbe dipendere da quella di altri elementi (es. sorted)

Poiché Stream opera su oggetti, esistono analoghe versioni ottimizzate per lavorare con 3 tipi primitivi: 
- Su int: _IntStream_
- Su double: _DoubleStream_
- Su long: _LongStream_

- **Binding statico e dinamico**
Il binding nei linguaggi di programmazione è il meccanismo che ci permette di effettuare l’associazione tra una variabile e il suo tipo (o in termini più semplici il task che ci permette di capire il tipo di una variabile).
Nel linguaggio Java esistono due tipi di binding:

- _statico_: avviene a tempo di compilazione del programma (dal compilatore javac).  Il binding è statico per:
	  - metodi statici: perchè appartengono alla classe stessa, non a un’istanza della classe. Il compilatore risolve la chiamata in base al tipo della variabile (tipo statico) e non all’oggetto effettivo a runtime. Poiché non c’è possibilità di sovrascrittura (overriding) per i metodi statici, il binding avviene durante la compilazione.
	  - metodi final non possono essere sovrascritti da classi derivate. Pertanto, il compilatore può risolvere quale metodo chiamare durante la fase di compilazione, poiché il metodo rimarrà lo stesso indipendentemente dall’oggetto effettivo.
	  - metodi private non sono visibili dalle classi derivate, quindi non possono essere sovrascritti
quindi riassumendo il binding è statico per tutti i metodi che non possono essere sovrascritti

- _dinamico_: avviene a runtime e viene effettuato dalla JVM. Avviene per i metodi non statici, non privati e non final.
Il metodo effettivo da invocare viene determinato a runtime in base al tipo concreto dell’oggetto su cui viene chiamato il metodo, non al tipo della variabile di riferimento.
il binding dinamico polimorfismo riguarda il comportamento degli oggetti e come i metodi sovrascritti vengono risolti a runtime in base al tipo effettivo dell’oggetto.

- **Collection**
Le collezioni in Java sono rese disponibili mediante il framework delle collezioni (Java Collection Framework)
Servono a memorizzare e organizzare i dati in memoria così da utilizzarli in modo efficiente

_Gerarchia delle interfacce Collection o gerarchia degli iterabili
- Interfaccia più generale: Iterable, che permette di iterare sugli elementi di una collezione
- Collection: l’interfaccia madre di tutte le collezioni in Java

poi si divide principalmente in 3 categorie
- Set: collezione non ordinata che non può contenere duplicati.
- List: collezione ordinata che può contenere duplicati.
- Queue: collezione FIFO (First In First Out).

Anche se Map non estende Collection, è comunque parte del framework delle collezioni in Java. Una Map memorizza coppie chiave-valore, dove ogni chiave è associata a un singolo valore.

diversi tipi di iterazione su una collezione:
- _iterazione esterna_: richiede che il programmatore controlli manualmente il flusso dell'iterazione. In questo approccio, il programmatore gestisce come e quando passare all’elemento successivo. Si fa attraverso iterator, il costrutto for each o mediante indici
- _iterazione interna_: il controllo del flusso dell’iterazione è delegato alla collezione stessa o a una funzione predefinita che esegue l’iterazione “al suo interno”. Essa avviene mediante il metodo `iterable.forEach`  e le funzioni di stream come forEach, map, filter, ecc.

Collezioni fondamentali
- ArrayList -> implementa la lista mediante un array
- LinkedList -> implementa la lista mediante elementi linkati
- HashSet -> memorizzano gli elementi in una tabella di hash
- TreeSet -> memorizza gli elementi in un albero mantenendo un ordine sugli elementi
- LinkedHashSet -> memorizza gli elementi in ordine di inserimento

Le mappe mettono in corrispondenza chiavi e valori
- HashMap -> memorizza le coppie in una tabella di hash
- TreeMap -> memorizza le coppie in un albero mantenendo un ordine sulle chiavi
- LinkedHashMap -> mantiene l'ordinamento di iterazione secondo gli inserimenti effettuati

_Interfacce built-in Java_
- `Predicate<T>`:  è una funzione che accetta un argomento generico T e restituisce un valore booleano (true o false). Viene tipicamente usata per esprimere condizioni o filtri.
- `Function<T, R>`: rappresenta una funzione che accetta un argomento di tipo T e restituisce un valore di tipo R. È spesso utilizzata per mappare un valore a un altro (trasformazioni o conversioni).
- `Supplier<T>`:rappresenta una funzione che non accetta argomenti e restituisce un valore di tipo T. È utilizzato quando abbiamo bisogno di “fornire” un valore, ma non abbiamo bisogno di input. Esempio generazione di un numero casuale
- `Consumer<T>`: è una funzione che accetta un argomento di tipo T ma non restituisce nulla. Viene utilizzata per operazioni che consumano un valore, come stampare, salvare o elaborare dati.

- **Design Pattern**
- _Strategy Pattern_: È un pattern secondo cui bisognerebbe progettare un'interfaccia funzionale per ogni comportamento e per ogni possibile tipo di comportamento implementare l'interfaccia. I comportamenti specifici devono essere impostati nel costruttore di ciascuna sottoclasse. Principio di design: preferisci la composizione all’ereditarietà

buona scelta: permette a ciascuna sottoclasse di implementare i comportamenti che effettivamente essa deve modellare
cattiva scelta: distrugge ogni possibile RIUSO del codice, perché – se non riusciamo a definire un metodo di default - dobbiamo reimplementare le interfacce per ogni sottoclasse

- _Factory Pattern_: la creazione degli oggetti viene separata dalla classe, che ne governa lo stato e i comportamenti. Così facendo si incapsulano costruttori, che diventano indipendenti e facilmente accessibili. È un pattern creazionale che ci permette di delegare il compito di costruire istanze di oggetti a una classe separata chiamata NomeClasseFactory. permette a una classe di differire l’istanziazione alle sottoclassi.

- _Builder Pattern_: Come il Factory Pattern è un altro pattern per la creazione di oggetti. Quando si hanno classi con tantissimi campi, molti dei quali possono avere dei valori di default, solitamente, si vanno ad elencare un gran numero di costruttori. Per evitare che questo accada, è stato inventato il pattern creazionale builder.

![[BuilderPattern.png]]

Vantaggi:
• Permette di rendere più flessibile la costruzione di oggetti con molti parametri
• Rende il codice di costruzione più leggibile
• Permette di evitare il passaggio di parametri null o poco chiari
• Permette di evitare di avere stati intermedi non validi dell'oggetto costruito

Svantaggi:
• La costruzione richiede più chiamate di metodi

- _Singleton Pattern_: permette di obbligare/vincolare la costruzione di un unico oggetto mediante un unico punto di accesso statico e un costruttore privato. Serve a rendere una Classe istanziabile una ed una sola volta.
1. Rende il costruttore di classe privato.
2. Crea un campo statico privato chiamato instance di tipo Classe. Il riferimento all’unico oggetto della classe.
3. Crea un metodo statico pubblico che crea / restituisce il riferimento all’unica istanza della classe.

Il Singleton pattern è utile quando vuoi assicurarti che ci sia una sola istanza di una classe e che questa istanza sia accessibile globalmente. È utilizzato in situazioni in cui avere più di una singola istanza della classe potrebbe causare problemi o non avrebbe senso. Un eccessivo numero di istanze può essere costoso a livello di risorse

- _Decorator Pattern_:
Il Decorator Pattern permette di estendere le funzionalità/responsabilità di una classe, senza modificare il codice della stessa
Il decorator aggiunge nuove responsabilità/funzionalità ad un oggetto senza che esso lo sappia. 
1. Creare una classe astratta Decorator che estenda il “Componente” (la classe astratta dell’oggetto).
2. Definire un campo del tipo “Componente” che venga valorizzato all’interno del costruttore del Decorator che accetta un riferimento a un Componente. 
3. In Decorator bisogna mantenere astratto il comportamento da decorare.
4. Concretizza i Decorator creando delle sottoclassi che dovranno implementare i metodi astratti definiti in Componente, potendo sfruttare il comportamento del componente che sto decorando e in più aggiungere qualcosa. I Decoratori concreti possono aggiungere dei campi che sono utili per effettuare la decorazione.

Il decoratore è un parassita che ingloba un componente, lo sfrutta senza che lui lo sappia aggiungendo qualcosa. “Nelle swing avete un esempio di decoratore che è il JScrollPane, mi sembra…” cit. Prof. Faralli da richiamare solo in caso di richiesta esplicita.
Vantaggi:
- Consente di rendere indipendenti la gerarchia dei Componenti da quella delle Decorazioni.
- Permette di estendere le funzionalità di una classe senza modificare il codice della stessa IMPORTANTE

Principio di Design: Le classi dovrebbero essere aperte all’estensione ma chiuse alla modifica

- _Command/Callback Pattern_: Per codificare funzioni da salvare in/passare a un oggetto e chiamare in seguito.
Alle volte è necessario effettuare delle richieste a oggetti senza sapere nulla relativamente all’operazione richiesta, facendo in modo che questo comportamento possa essere specificato in un secondo momento (anche a runtime).

Per fare ciò, è necessario rendere l’operazione modulare in modo che possa essere associata a un oggetto

1. Crea delle interfacce funzionali chiamate Callback.
2. Nella classe che deve implementare e utilizzare quel comportamento dichiara un riferimento a un oggetto del tipo dell’interfaccia Callback su cui sarà possibile richiamare il metodo.
 ![[Screenshot 2024-09-17 at 21.10.29.png]]

- **Classi Wrapper**
Le classi wrapper in Java sono delle classi che permettono di convertire i tipi primitivi in oggetti.
Questo è necessario quando si lavora con strutture dati come le collezioni, che accettano solo oggetti e non tipi primitivi, quindi i tipi primitivi devono essere convertiti nelle loro classi wrapper corrispondenti.
Ogni tipo primitivo ha una corrispondente classe wrapper:
• int → Integer
• char → Character
• boolean → Boolean
• double → Double
ecc.
_Autoboxing e Unboxing_
Con Java 5 è stata introdotta una funzionalità chiamata autoboxing, che consente la conversione automatica tra tipi primitivi e le loro classi wrapper. Ad esempio, se si aggiunge un valore int a una collezione che accetta solo oggetti, Java converte automaticamente l’int in un oggetto Integer. Questa conversione inversa da wrapper a primitivo è chiamata unboxing.

Le classi wrapper includono metodi utili, come:
• `valueOf()`: converte un valore primitivo in un oggetto wrapper.
• `intValue()`, `doubleValue()`, ecc.: convertono un oggetto wrapper nel corrispondente valore primitivo.

- **Downcasting e Upcasting**
L’_upcasting_ avviene quando un oggetto di una classe figlia viene trattato come se fosse un oggetto della sua classe padre. Questo avviene implicitamente, cioè non è necessario specificare il cast in modo esplicito. È utile quando si vuole scrivere codice che sia generico e possa lavorare con oggetti di più classi, sfruttando il polimorfismo.

quando si fa upcasting ( è il processo di conversione (o “cast”) di un oggetto di una sottoclasse a un riferimento della sua superclasse), si possono chiamare solo i metodi e vedere solo i campi della superclasse

Il _downcasting_ è il processo inverso dell’upcasting, cioè quando si prende un riferimento di una classe padre e si converte esplicitamente in un riferimento di una classe figlia. A differenza dell’upcasting, questo tipo di cast deve essere fatto in modo esplicito e può generare errori di runtime se non viene verificato correttamente.

Differenze principali:
• _Upcasting_: viene fatto automaticamente e non richiede alcun cast esplicito.
• _Downcasting_: richiede un cast esplicito e può generare errori se non viene eseguito correttamente.

In sintesi, l’upcasting rende il codice più flessibile e generalizzato, mentre il downcasting viene utilizzato per accedere a comportamenti specifici della sottoclasse

- **Eccezioni**
Le eccezioni rappresentano un meccanismo utile a notificare e gestire gli errori, indicano che durante l'esecuzione si è verificato un'errore.

gli errori si dividono in:
- _sincroni_: si verificano a seguito dell'esecuzione di un'istruzione, a sua volta si dividono in non critici (errori che derivano da condizioni anomale come la divisione per 0) e errori critici (errori interni alla JVM come conversione di tipo non consentito)
- _asincroni_: accadono parallelamente all'esecuzioni e sono quindi indipendenti al flusso di controllo (es. click del mouse)

gli unici errori che possono essere gestiti attraverso le eccezioni sono gli errori sincroni

blocco try e catch:
- nel blocco try si inseriscono tutte le istruzioni dalle quali vengono sollevate le eccezioni che vogliamo catturare
- nel blocco catch invece è necessario indicare il tipo di eccezione da catturare e specificare nel blocco le azioni da attuare a seguito dell'eccezione sollevata

E’ molto importante considerare l’ordine con cui si scrivono i diversi blocchi catch e catturare le eccezioni dalla più specifica a quella più generale

_politica catch-or-declare_
Una volta sollevata un’eccezione, possiamo:

- Ignorare l’eccezione e propagarla al metodo chiamante, a patto di aggiungere all’intestazione del metodo la clausola
_throws_, seguìto dall’elenco delle eccezioni potenzialmente sollevate (_declare_)
- Catturare l’eccezione, ovvero gestire la situazione anomala in modo opportuno, prendendo provvedimenti e contromisure atte ad arginare il più possibile la situazione di emergenza (_catch_)

se vogliamo ignorare le eccezioni è necessario usare `throws`, esso dichiara che il metodo o i metodi delle classi da questo invocati potrebbero sollevare eccezioni dello stesso tipo di quelle elencate dopo throws

Se tutti i metodi all’interno dell’albero delle chiamate dell’esecuzione corrente decidono di ignorare l’eccezione, l’esecuzione viene interrotta

_Eccezioni personalizzate_
```Java
public class MiaEccezione extends Exception {

}
```

Tramite la parola chiave `extends` è possibile creare una nuova eccezione a partire da un tipo già esistente
Tramite la parola chiave `throw new` è possibile sollevare (o lanciare) una nuova eccezione

L’eccezione personalizzata  nasconde i dettagli implementativi e trasmette un significato appropriato al contesto

`finally` è un’altra parola riservata del linguaggio Java che ci consente di definire un blocco di istruzione da eseguire in ogni caso, solitamente effettua delle operazioni di clean up.

![[GerarchiaEccezioni 1.png]]

La classe che implementa il concetto di eccezioni è `Throwable` che estende direttamente la classe Object e si trova in cima alla gerarchia delle eccezioni. Gli oggetti di tipo Throwable sono gli unici oggetti che è possibile utilizzare con il meccanismo delle eccezioni.

poi ci sono le classi `Exception` e `Error`:
- _Exception_: per le eccezioni interne alla JVM legate ad errori nella logica del programma
- _Error_: cattura l’idea di condizione eccezionale irrecuperabile (es ThreadDeath, OutOfMemoryError...)

_Eccezioni di tipo checked e unchecked_:
- Le eccezioni checked sono quelle comuni che estendono Exception (ma non Runtime Exception) per cui è obbligatorio attenersi al paradigma catch or declare.
- Le eccezioni unchecked sono eccezioni che estendono Error o RuntimeException non è obbligatorio sollevarle o catturarle in un blocco try-catch sebbene sia possibile.

## Concetti da ricordare
- ogni oggetto è l'istanza di una classe
- la differenza tra i tipi primitivi e oggetti è il fatto che nel primo caso la memoria viene allocata automaticamente a tempo di compilazione, mentre negli oggetti questa viene allocata durante l'esecuzione del programma