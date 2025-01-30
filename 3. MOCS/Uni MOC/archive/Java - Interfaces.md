---
type: Uni Note
class: 
academic year: 2023/2024
related: 
completed: true
created: 2024-06-17T15:30
updated: 2025-01-30T18:01
---
## Introduzione 

Le interfacce sono uno strumento fornito da java per risolvere il problema dell'*eredità multipla*, non è possibile estendere più di una classe, ma è possibile implementare più di un interfaccia.

Infatti non possono essere istanziate ed il loro obbiettivo è quello di fornire dei metodi che devono essere implementati da una classe concreta, (le classi astratte non devono fornire un implementazione dei metodi).

Le classi possono contenere:
- **Metodi** senza implementazione che sono implicitamente `abstract` e `public`
- **Campi costanti** che sono implicitamente `public`, `static` e `final`
- **Metodi di Default**  con implementazione ma che sono implicitamente `public`e  `static`

Un interfaccia può estendere un altra interfaccia ed ereditare tutti i sui metodi, di cui tutti quelli non di default dovranno essere implementati dalla classe che implementa l’interfaccia

>[!warning] Differenza tra Interfacce e classi astratte
>
>**Ereditarietà:** una classe può estendere solo una altra classe, ma implementare molteplici interfacce.
>
>**Metodi:**
>- Nelle ***Interfacce*** sono `astract` e `public`, se di default allora `public`, `static` e `final`.
>- Nelle ***Classi Astratte*** posso avere *qualsiasi visibilità* ed essere *astratti* o *concreti*.
>
>**Attributi:**
>- Nelle ***Interfacce*** sono `statici` e `finali`.
>- Nelle ***Classi Astratte*** possono avere *qualsiasi visibilità* ed essere *static* o non static.

---
## Implementazione

Implementare un interfaccia significa creare una classe che implementa i metodi (astratti) contenuti dall'interfaccia

>[!note] Esempio
>```java
>public class Cerchio implements FormaGeometrica {
>   private double raggio;
>   
>   public Cerchio(double raggio) {
>      this.raggio = raggio;
>   }
>   
>   @Override
>   public double area() {
>      return PI * raggio * raggio;
>   }
>   
>   @Override
>   public double perimetro() {
>      return 2 * PI * raggio;
>   }
>}
>```
>In questo esempio, abbiamo definito una classe `Cerchio` che implementa l'interfaccia `FormaGeometrica`. La classe `Cerchio` deve fornire una implementazione per i metodi `area()` e `perimetro()` definiti nell'interfaccia.

### Metodi Default e Statici 

Le interfacce possono anche contenere metodi di default e statici, che possono essere implementati direttamente nell'interfaccia stessa. 

>[!warning] Metodi di Default
>Definendo metodi con implementazione di default all'interno delle interfacce diamo la libertà a chi implementa l'interfaccia di scegliere se sovrascrivere il metodo di default o utilizzare l'implementazione predefinita.

>[!warning] Metodi Statici
>Definendo metodi statici all'interno delle interfacce. Questi metodi possono essere chiamati utilizzando il nome dell'interfaccia seguito dal nome del metodo.

>[!note] Esempio
>```java
>public interface FormaGeometrica {
>   double PI = 3.14;
>   
>   default double areaCirconferenza(double raggio) {
>      return PI * raggio * raggio;
>   }
>   
>   static double areaQuadrato(double lato) {
>      return lato * lato;
>   }
>   double area();
>   double perimetro();
> }
>```

---
## Eredità Multipla

Java supporta l'ereditarietà multipla tramite le interfacce. Una classe può implementare più di un'interfaccia, consentendo così di ereditare comportamenti da più fonti.

Tuttavia, Java non supporta direttamente l'ereditarietà multipla per le classi. Ciò significa che una classe in Java può estendere solo una singola classe base. Tuttavia, Java supporta l'ereditarietà multipla indiretta attraverso l'utilizzo di interfacce.

>[!note]- Esempio
>```java
>public interface Forma {
>   double PI = 3.14;
>   double area();
>}
>
>public interface Stampabile {
>   void stampa();
>}
>
>public class Cerchio implements Forma, Stampabile {
>   private double raggio;
>   
>   public Cerchio(double raggio) {
>      this.raggio = raggio;
>   }
>   
>   @Override
>   public double area() {
>      return PI * raggio * raggio;
>   }
>   
>   @Override
>   public void stampa() {
>      System.out.println("Stampo il cerchio con raggio " + raggio);
>   }
>}
>```

---
## Estendibilità

Le interfacce possono estendere altre interfacce, consentendo la creazione di gerarchie di interfacce. Una classe che implementa un'interfaccia estesa deve fornire implementazioni per tutti i metodi definiti nelle interfacce padre.

>[!note]- Esempio
>
>```java
>
>public interface Forma {
>   double PI = 3.14;
>   double area();
>}
>
>public interface Stampabile {
>   void stampa();
>}
>
>public interface FormaStampabile extends Forma, Stampabile {
>   double perimetro();
>}
>
>public class Cerchio implements FormaStampabile {
>   private double raggio;
>   
>   public Cerchio(double raggio) {
>      this.raggio = raggio;
>   }
>   
>   @Override
>   public double area() {
>      return PI * raggio * raggio;
>   }
>   
>   @Override
>   public void stampa() {
>      System.out.println("Stampo il cerchio con raggio " + raggio);
>   }
>   
>   @Override
>   public double perimetro() {
>      return 2 * PI * raggio;
>   }
>}
>```
>
>In questo esempio, l'interfaccia `FormaStampabile` estende le interfacce `Forma` e `Stampabile`, il che significa che una classe che implementa `FormaStampabile` deve fornire implementazioni per i metodi astratti `area()` e `stampa()` ereditati da `Forma` e `Stampabile`, nonché per il metodo astratto `perimetro()` definito in `FormaStampabile`.

