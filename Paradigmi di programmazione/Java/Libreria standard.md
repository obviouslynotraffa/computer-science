
Per affrontare ampiamente questo tema, è necessario prima introdurre alcune caratteristiche della librearia messa a dispozisione del linguaggio.

## Moduli
Stiamo parlando della documentazione, ovvero dei *JavaDoc*. Un modulo è un insieme di package e tipi, di cui si può controllare l'accesso esterno. Si tratta, di fatti, di una organizzazione del codice Java **superiore** al package.

Il principale uso dei moduli è la modularizzazione della piattaforma java, ovvero, consentono di separare il JDK in parti più piccole che contengono solo i moduli necessari, rendendo la pubblicazione più agevole. Quindi si possono togliere librerie non necessarie.

## I/O
Il modello di I/O di Java è simile al modello POSIX comune e a molte librerie standard, che è contenuto nel package java.io. Le principali astrazioni sono il File, l'InputStream e l'OutputStream, da cui derivano le varie implementazioni.

Gli usi più comuni sono attraverso le classi Reader e Writer, che forniscono metodi semplici per la scrittura e la lettura di file testuali. 

```java
BufferedReader rd = new BufferedReader(new FileReader(".hgignore"));
String line= rd.readLine();
while(line!=null){
	System.out.println(line);
}
rd.close();
```

La libreria standard è organizzata per gerarchia di capacità e promuove l'uso della composizione per costruire le catene di elaborazione necessarie. La gerarchia è molto orientata agli oggetti, infatti ogni classe fa il minimo.

## Collections
La più importante della libreria standard è la libreria di Collezioni, che sono usate diffusamente in tutto il sistema e che ha ricevuto un importante aggiornamento nella versione 8.

L'interfaccia `Collection` è la radice della libreria, contiente i metodi più generali, che tutte le interfacce più specifiche includono. Non ci sono implementazioni dirette in questa interfaccia, ma solo nelle più specializzate.

La maggior parte delle collezioni distingui i contenuti nel senso del metodo `java.lang.Object#equals()`, che quindi è necessario implementare correttamente in questi casi. Di fatti, l'operatore di confronto `==` non è utilizzabile fra gli oggetti, in quanto confronta solo l'identità: due istanze della stessa isdentità saranno sempre diverse, anche se hanno gli stessi campi dati. L'operatore restituirà true quando vengono confrontati due istanze che sono esattamente la stessa, che magari hanno nome diverso per dei riferimenti.

```java
class Point{
	public int x,y;
	
	Point(int x, int y){
		this.x=x;this.y=y;
	}
	
	Point TwoTimes(){
		x*=2;y*=2;
		return;
	}
}
```
```java
Point a = new Point(2,1);
Point b= new Point(3,4);
Point c= new Point(2,1);

a==b //false
a==a //true
a==c //false
a==a.TwoTimes() //true


```

Si può tuttavia, overridare il metodo `==`, un po come in C
```java
@Override
public boolean equals(Object other){
	if (other istanceof Point){
		Point o =(Point) other;
		return this.x==o.x && this.y==o.y;
	} else return false;
}

@Override
public int hashCode(){
	return (x & 0xffff) << 16 + (y & 0xffff);
}

```
```java
Point a = new Point(2,1);
Point b= new Point(3,4);
Point c= new Point(2,1);

a==b //false
a==a //true
a==c //false
a.equals(c) //true
a==a.TwoTimes() //?
```


La classe Collections raccoglie diversi metodi di utilità per applicare algoritmi alle collezioni, o per aggiungere particolari funzioni alle già esistenti:
- `checkedTTT`: controlla a run-time il tipo
- `emptyTTT`: collezione vuota
- `syncronizedTTT`: collezione sincronizzata
- `unmodifiableTTT`: vista non modificabile

- `binarySearch`: ricerca in una lista
- `disjoint`: verifica che siano disgiunte (nessun elemento in comune)
- `fill`: riempe la collezione di uno stesso oggetto/valore
- `min`, `max`: trova min/ma
- `reverse`: inverte l'ordine
- `shuffle`: ordina in modo casuale
- `sort`: ordina la collezione



## Iterator / Iterable
Un `iterator` consente di elencare una collezione un elemento alla volta, individuando quando la si è attraversata completamente (come in C, praticamente). Si può pensare come ad un puntatore che punta ad un sigolo elemento della collezione, e che con i metodi si sposta vanti e indietro . Una classe `iterable`, può fornire un iterator per essere attarversata.

Metodi **iterator**:
- `next`: prossimo elementi
- `hasNext`: vero se il next non è nullo
- `remove`: rimuove il nodo corrente
- `forEachRemaing`: consuma il resto della collezione (nel senso che prima fai delle cose, poi quando hai raggiunto il goal, fai altre cose nel resto)


Metodi iterable:
- `forEach`: lo fa per ogni elemento
- `iterator`: fornisce un iterator
- `spliterator`: fornisce uno spliterator che abilità l'iterazione parallela


## List
L'interfaccia `List` rappresenta un elenco ***ordinato*** di elementi, indirezzabili per ***posizione***. Sono permessi duplicati. Viene fornito uno specifico iteratore, `ListIterator`, capace di muoversi avanti e indietro.

- `ArrayList`: basata su un array
- `LinkedList`: basata su nodi concatenatu
- `Vector`: legacy

Fornisce anche un metodo che permette di creare rapidamente una lista a partire da un elenco di oggetti.
```java
var list = List.of(1, 2, 3);
```


## Set
L'interfaccia `Set` definisce un insieme, cioè un contenitore di oggetti ***senza ripetizioni*** (se uno oggetto che è gia dentro al set viene inserito, si ignora) e non ***ordinato*** (le iterazioni attraverso la stessa lista, avvengono in maniera diversa e non in ordine). É una pessima idea, quella di cambiare un elemento in un set in modo che cambi il suo significato riguardo a equals: potresti non essere più in grado di recuperare l'oggetto.

- `HashSet`: basato su HashMap
- `LinkedHashSet`: ordinato in inserimento
- `TreeSet`: dotato di ordine interno
- `EnumSet`: specializzato per le enum
- `SortedSet`: è definito un ordine totale (possibile individuare inizio e fine)
- `NavigableSet`: è possibile muoversi basandosi sull'ordine


## Dequeue
L'interfaccia `Dequeue` rappresenta una Double Ended Queue, cioè una struttura dati in cui è possibile aggiungere o togliere elementa da uno dei due estremi. Caratteristica della `Dequeue` è avere due set di metodi differenti a seconda del comportamento in caso di impossibilità dell'azione richiesta:
- `add`, `remove`, `get` : se impossibilitate nel farle, ritorna un eccezione
- `offer`, `poll`, `peek`: ritornano rispettivamente: booleano, null, null


## Map
Un'interfaccia `Map`, rappresenta un'associazione chiave-valore. Gli oggetti usati come chiavi devono avere la coppia equals/hashCode correttamente definita. Sono solo permesse chiavi uniche. Ha quasi gli stessi metodi sopra e anche lui definisce un metodo per consentire di costruire rapidamente una mappa.

```java
var map = Map.of("A",1 ,"B",2 ,"C",3);
```


## Stream
Da Java 8 il concetto di `Stream` è entrato in modo pervasivo nella libreria di Java. A molte interfacce è stato aggiunto un metodo `stream()` che permette di trattare le collezioni in modo particolare. Uno stream è una sequenza di elementi, non necessariamente finita. L'obiettivo dello stream è la descrizione dei passi di elaborazione che verranno effetuati sugli elementi e l'ottimizzazione della loro esecuzione.

Le operazioni sugli stream vengono composte in sequenza, in una ***pipeline***, fino ad arrivare ad una operazione detta ***terminale*** che produce il risultato. Nessuna operazione viene eseguita finché non viene richiamata l'operazione terminale.

Il codice che implementa la pipeline ha ampie libertà su come disporre l'esecuzione delle operazioni intermedie. Queste  devono:
- non modificare gli elementi dello stream
- non avere uno stato interno

Le operazioni intermedie sugli stream si dividono in

- ***stateful***
	- distinct: elementi distinti
	- concat: concatena due stream
	- limit: tronca lo stream
	- skip: salta l'inizio dello stream
	- sorted: ritorna lo stream ordinato
- ***stateless***
	- filter: solo gli elementi che soddisfano il predicato
	- drop/takeWhile: escludi/mantieni, finchè vale il predicato
	- map: trasforma ogni elemento
	- peek: esegue un'operazione senza consumare l'elemento
