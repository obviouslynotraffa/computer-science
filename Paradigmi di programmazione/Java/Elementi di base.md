In Java, l'unità principale di organizzazione del codice è la Classe. Ma non è l'unica. Altri costrutti arricchiscono il sistema dei tipi di Java, o sono stati aggiunti nel tempo inrisposta all'evoluzione del mercato e della pratica.


## Interfacce
Una interfaccia dichiara le caratteristiche di un Tipo senza fornire una sua implementaizione (come le classi astratte in C++). Le classi che usano le interfacce possono dichiarare di implementare una funzione fornendo l'implementazione richiesta.

```java 
package it.unipd.pdp2023;

interface Baz{
	int test=1;
	void bar();
	String desc(boolean b);
}

class Foo extends App implements Baz{
	private String a;
	void bar() {};
	String desc(boolean b){return "";}
}
 ```
In questo caso, la classe *Foo* è obbligata a fornire una implementazione di *desc()*, a meno di non essere astratta.


Le interfacce in Java permettono di avere una sorta di ereditarietà multipla mitigando il Diamond Problem. Una classe può estendere una sola altra classe, ma implementare molte interfacce. E comune, per esempio, che una libreria fornisca un insieme di interfacce per affrontare un certo problema, ed un insieme più ampio di implementazioni con caratteristiche differenti, che possono essere selezionate al runtime a seconda delle circostanze. Il codice utilizzatore non dipende dalla implementazione, ma può usare quella che gli viene fornita. L'assimmetria con l'ereditarietà di classi consente di risolvere le ambiguità. 


Una interfaccia può essere implementata da più classi, ma essere estesa solo da un altra interfaccia. Può avere una visibilità pubblica o package, tutti i suoi membri sono pubblici di default.


Un'interfaccia può contenere:
- dichiarazioni di costanti
- metodi astratti
- metodi statici
- ***metodi di default***
- metodi privati

Ogni variabile dichiarata in una interfaccia è implicitamente *public static final*, vale a dire costante. Non è necessario indicare un metodo come abstract.

Alle interfacce viene permesso di avere dei default method, cioè dei metodi che si comportano in modo simile alle superclassi. Un metodo di default viene prefissato dalla parola chiave default e viene fornita la sua implementazione. Questo è stato fatto per evitare di rifare sempre il codice quando si cambiano le librerie.

```java 
package it.unipd.pdp2023;

interface Top{
	default String name() {return "unname";}
}

interface Left extends Top{
	default String name() {return getClass().getName();}
}

interface Right extends Top{}

interface Bot extends Left, Right {}

//In questo caso, Bot usa l'implementazione di Left in quanto più vicina in senso ereditario. Le regole per leinterfacce sono separate da quelle delle classi.
 ```

Tutttavia, il *Diamond problem*, si ripresenta: viene rilevato al momento della compilazione, se la gerarchia di ereditarietà ed implementazioni di una classe porta ad una ambiguità nella selezione di un metodo, il compilatore segnala un errore, che può essere risolto solo modificando il codice.


#### Annotazioni
Un interfaccia il cui nome inizia con "@" diventa di un tipo particolare, detto *annotazione*. Le annotazioni si possono applicare sintatticamente a metodi, classi e variabili, e sono disponibili al momento dell'esecuzione.
Il loro scopo è arricchire di *metadati* la struttura a cui sono applicate, in modo da consentire la rilevazione e l'uso durante la compilazione o l'esecuzione.

Alcune annotazioni della libreria standard:
- *@Deprecated* : segnala un metodo che verrà rimosso in futuro
- *@Override* : segnala un membro che sostituisce o implementa un membro di una superclasse
- *@SupressWarnings* : istruisce il compilatore a nascondere i warning
- *@FunctionalInterface* : indica al compilatore che l'interfaccia può essere usata in modo funzionale


```java 
package it.unipd.pdp2023;

class Foo extends Bar{
	@Override
	String methodB() {return "";}
	
	@Override
	@Deprecated
	int methodOld() {return 0;}
	
	@SupressWarnings
	private boolean b=false;
}

 ```



## Tipi generici
Un aggiornamento importante, è quello in cui hanno introdotto i cosidetti "*Generics*" (i template in C++). Una classe o un interfaccia generica dichiara uno o più parametri che possono essere specificati nel momento della sua istanziazione.

```java 
package it.unipd.pdp2023;

interface MappableList<T>{
	void add(T element);
	T head();
	List<T> tail();
}
 ```

All'interno della definizione, il parametro T può essere usato come un tipo. Al momento della creazione di una istanza della classe, dell'implementazione dell'interfaccia o della chiamata del metodo, è necessario specificare un tipo concreto al posto del parametro.


E' possibile non esprimere vincoli sui parametri, ma solo sul tipo parametrizzato:
```java
package it.unipd.pdp2023

class Test{
	static void printCollection(Collection<?> c){
		for (Object o:c){
			System.out.printIn(o);
		}
	}
}
```

In questo caso, non ho necessità di condizionare il contenuto della collezione. Mettendo la wildcard `?` esprimo alcompilatore questa mia intenzione.

L'uso più comune di questo costrutto avviene nella libreria standard delle Collezioni, ovvero tutte le implementazioni dei tipici contenitori: liste, insiemi, code. L'uso dei generici permette di evitare di duplicare il codice, e di semplificare l'uso delle classi contenitore fornendo al compilatore informazioni riguardo al tipo di ritorno di alcuni metodi. Purtroppo, a causa di problematiche di compatibilità con il codice precedente, le informazioni sui tipi generici vengono cancellate al runtime e non sono più disponbili dopo la compilazione. Questo è stato ungrosso cruccio per molte librerie e strumenti che cercavano di implementare algoritmi generalizzati su più tipi.


## Tipi primitivi
Non tutto in Java è un oggetto. Come retaggio del suo iniziale focus verso le piattaforme embedded, i tipi di dato fondamentali non sono oggetti ma vengono detti valori primitivi.

| universo   | tipo corto       | tipo lungo |
| --------- | ---------------- | ---------- |
| Interi    | byte, short, int | long       |
| Decimali  | float            | double     |
| Caratteri | char             |            |
| Booleani  | boolean          |            |

La `String` non è un tipo primitivo, ma un oggetto !

Un valore primitivo non è un oggetto: nella sintassi non è trattato allo stesso modo ed un tipo primitivo non può essere indicato come parametro di tipo. Ogni tipo primitivo ha quindi un corrispettivo Tipo non primitivo che può essere usato per trasportare lo stesso valore nelle situazioni in cui sia necessario.

Prima di Java 5 la conversione doveva essere fatta manualmente (con grande dispendio di codice). In Java 5 è stato introdotto il concetto di *autoboxing*: il compilatore riconosce il contesto in cui il valore primitivo (o del corrispondente tipo) viene usato e applica la trasformazione necessaria.

Gli `array` invece sono oggetti 
```java
package it.unipd.pdp2023

class Foo{
	int[] array;
	
	Foo(){
		array = new int[10];
		array[0]= 42;
	}
}
```


## Enumerazioni
Una `enum` è una particolare categoria di classi: rappresenta un tipo contenente un numero determinato di elementi, definiti alla dichiarazione. 

```java
package it.unipd.pdp2023

enum Category{A, B, C, D;}

Category cat = Category.A;
```

Una classe enum ha automaticamente alcuni metodidi utilità per interrogare l'insieme dei suoi valori. Formalmente, una classe E di questo tipo deriva da `Enum< E >`. Non è possibile istanziare una enumerazione, solo usare i suoi valori. Gli elementi dell'enumerazione sono le uniche istanze della classe che li rappresenta. Se una enumerazione è una classe interna, è implicitamente `static`.

L'enumerazione può dichiarare variabili, metodi, o implementare interfacce, e queste caratteristiche si riflettono sugli elementi in quanto istanze della classe. Se nessun elemento dichiara una implementazione specifica, l'intera enum si considera `final`. Se uno o più ce l'hanno, l'intera enumerazione non lo è.


## Records
Sono delle strutture dati, lontane parenti delle `struct` del C. La dichiarazione di un **record** è semplice:
```java
record Name (String Name, String Surname){}
```
l Record è anche implicitamente `final`, quindi non può essere astratto nè essere esteso. Un record interno adun'altra classe è anche implicitamente `static`. Il record è immutabile, i valori non possono essere cambiati.

E' possibile definire metodi in un record, o reimplementare uno dei metodi generati automaticamente. E' possibile dichiarare un record generico o implementare una interfaccia. In questo modo, il record diventa una scorciatoia per definire tutte le classi che normalmente modellano valori di dominio che vengono trasportati da un posto all'altro del sistema.