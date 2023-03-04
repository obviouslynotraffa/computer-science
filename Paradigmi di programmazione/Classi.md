
In Java, l'*unità* principale di organizzazione del codice è la **Classe**. Ogni oggetto fa necessariamente riferimento alla definizione di una Classe, che **determina** la struttura del suo stato ed il codice che opera su tale stato.

Esistono varie categorie di clssi in Java, e di tanto in tanto ne vengono introdotte di nuove. Complessivamente, formane l'insieme dei tipi che il compilatore riconosce in un programma Java.


Una classe in Java è dichiarata dalla parola chiave *class* seguita dal nome della classe in ***PascalCase***.
```java 
class App{

}
 ```



### Package
Una classe appartiene ad un *package*, che permette do organizzare le classi in gruppi gerarchici.
```java 
package it.unipd.pdp2023;

class App{

}
 ```
La parola chiave *package* deve essere la prima riga del file. E' la omonima della directory in cui è situato il file. Per interderci è il namespace di C++. Per convenzione, i package sono denominati con nome di dominio, in ordine inverso.

In tal modo, la combinazione dell'organizzazione dei package in cartelle e delle classi in file omonimi rende la compilazione di un insieme di sorgenti Java un processo deterministico. Infatti il compilatore, dato un nome, sa semrpe dove trovarlo.



### Visibilità
Una classe non può usare un'altra classe qualsiasi: deve dichiarare l'intenzione di usarla e deve avere la visibilità giusta. Ogni classe, nella sua definizione, indica visibilità, ovvero la politica di accesso che intende concedere alle altre classi.

- ***Visibilità di default***: in mancanza di indicazioni, una classe è visibile da parte di tutte le classi dello stesso package, ma non alle classi al di fuori di esso. Una classe può usare un'altra classe all'interno dello stesso package senza particolari indicazioni.

- ***Visibilità pubblica***:  la classe è visibile da qualsiasi altra classe della JVM
```java 
package it.unipd.pdp2023;

public class App{
}
```

Un file sorgente può contenere al *massimo una classe pubblica* e deve chiamarsi come tale classe. Usando poi la direttiva *import* si aggiunge al file sorgente  il nome della classe importata.
```java 
package it.unipd.pdp2023;
import it.unipd.pdp2023.Util;

public class App{
	Util a;
}
```



### Struttura
Una classe può contenere diverse cose, tra i quali variabili, metodi, altre classi e blocchi di codice anonimi. Adesso li descriveremo brevemente.

###### Variabili
Una classe può contenere diverse variabili che definiscono la struttura di ciascun oggetto della classe. 
```java 
package it.unipd.pdp2023;

public class App{
	string a, a2=5, c;
	int b;
}
```

Le variabili si dividono in due categorie:
- **statiche**: ne esiste una sola copia, legata all'istanza classe (sono tipo le variabili globali).
- d'**istanza**: ogni oggetto ha la propria e fa parte del suo stato.
```java 
package it.unipd.pdp2023;

public class App{
	static char c;
	int b;
}
```
Le variabili statiche vengono inizializzate ed allocate nel momento in cui la classe viene caricata dal ClassLoader e preparata per l'uso. Per le variabili statiche ci accedo con la classe, mentre per quelle d'istanza con l'oggetto di invocazione.


Le variabili hanno più classi di visibilita:
- *public*: possono essere lette e scritte da ogni classe;
- *protected*: possono essere lette e scritte da classi che derivate;
- *default*: possono essere lette e scritte da classi dello stesso package;
- *private*: possono essere lette e scritte solo dalla classe stessa;

```java 
package it.unipd.pdp2023;

public class App{
	public static char c;
	int a;
	protected string internal;
	private boolean secter;
}
```



Ci sono inoltre altri modificatori che influsicono sulle variabili:
- *final*: il valore delle variabile non può essere cambiata dopo l'assegnamento, e il valore deve essere asseganto alla costruzione;
- *transient*: la variabile va ignorata in sede di serializzazione;
- *volatile*: la variabile ha un comportamento particolare in relazione all'accesso concorrente;

> Tutte le variabili vanno sempre scritte in **camelCase**, tranne le variabili stati final, che sono delle vere e proprie costatnti; il loro nome si scrive in MAIUSCOLO con il separatore underscore __.




###### Metodi
Una classe organizza il codice in metodi, che sono delle funzioni della classe. Un metodo è definito da:
- alcuni modificatori
- parametri di tipo
- tipo di ritorno
- un nome
- elenco dei parametri 
- blocco di codice da eseguire
```java 
package it.unipd.pdp2023;

public class App{
	public App();
	int apply(char d) {return 0;}
	static boolean prepare(String target, int n)
		throws RuntimeExceptions {
		return false;
	}
}
```
Una classe può avere uno o più metodi denominati come la classe stessa e sono chiamati costruttori. Un costruttore viene chiamato quando si richiede la creazione di un oggetto della classe.

La tupla formata da :
- nome del metodo
- parametri di tipo 
- elenco dei tipi degli argomenti
è detta firma (*signature*) del metodo. Una classe non può avere più metodi con la stessa firma.


Un metodo dichiarato static è legato alla classe: non può essere richiamato su un oggetto e non ha  accesso alle variabili d'istanza. I metodi seguono le stesse classi di visibilita delle variabili.


Un costruttore viene chiamato con la parola chiave *new*, e ritorna un oggetto della classe. 
```java 
boolean p = App.prepare("baz",1);
App a = new App();
app.apply("z");
```
Una classe ha sempre un costruttore di default, quando viene esplicitato un altro costruttore, quello di default non viene generato.



##### Classi interne
Una classe può dichiarare come membro una o più classi, queste vengono comunemente chiamate *NestedClasses*. Come le variabili ed i metodi possono essere statiche o meno e hanno una delle quattro descritte.

Le classi interne possono essere statiche o non e hanno comportamente profondamente diversi, tanto da essere chiamati:
- *static nested classes*: non hanno accesso privilegiato ai membri della classe ospite. Le classi static nested sono spesso legate a qualchedesign pattern (per es. Builder o Factory). Sebbene possano anche essere scritte al di fuori della classeospitante, può essere più chiaro a volte includerle perrendere più apparente il legame esistente.
```java 
package it.unipd.pdp2023;

public class App{
	static class Foo{
		int a;
	}
	static String b;
}
```

- *inner classe*: è una parte dell'oggetto ospitante, quindi ha lo stesso ciclo di vita dell'oggetto e ha privilegi sui membri dell'ospite. Non può dichiarare membri static. Le classi inner sono il segnale di un modello datiparticolarmente complesso. Si usano con particolare cautela. 
```java 
package it.unipd.pdp2023;

public class App{
	class Bar{
		int a;
	}
	String s;
}

App a = new App();
App.Bar b = a.new Bar();
```


##### Inizializzatori
In una classe possono essere contenuti anche blocchidi codice anonimi. Vengono eseguiti in sede di inizializzazione di unaclasse o di un oggetto.

- ***Inizializzatori statici***: blocchi di inizializzazione dichiarati static vengono eseguiti, in ordine di dichiarazione, al caricamento della classe. Il codice deve essere veloce e non deve fallire. Sono usate poco.
```java 
package it.unipd.pdp2023;

public class App{
	static String s="foo";
	static int l;
	
	static {
		l=s.lenght();	
	}
}
```


- ***Inizializzatori d'istanza***: sono privi di indicazioni sono eseguiti, in ordine lessicale, durante la creazione diciascuna istanza di oggetto della classe. In particolare, sono eseguiti dopo il supercostruttore ma prima di qualsiasi costruttore. 
```java 
package it.unipd.pdp2023;

public class App{
	static String s="foo";
	static int l, s;
	
	App(int param){
		j=param;
	}
	
	{ l=s.lenght();}
	
}
```



### Ereditarietà
Java, come linguaggio OO, mette a disposizione un meccanismo di ereditarietà singola: una classe può avere una sola superclasse, di cui eredita codice ( e parte) dello stato. Una sottoclasse ha accesso ai membri pubblici, package e protected della superclasse, ma non ai membri private.
```java 
package it.unipd.pdp2023;

public class App{
	private int a;
	protected int b;
	
}


class Foo extends App{
	private String c;
}

```


Limitandosi all'ereditarietà singola, Java ha evitato (in passato) il "***Diamond Problem***": è immediatamente individuabile a quale classe della gerarchia forniscel'implementazione di un metodo. Parte dei vantaggi dell'ereditarietà multipla vienere cuperata con altri meccanismi.

Una sottoclasse è anche un sottotipo della classe che estende. Può cioè essere usata in ogni posto in cui viene richiesta la classe superiore. 

> Per costruzione, tutti i metodi in Java sono "virtual"nel senso che ha il termine in C++. Vale a dire, il codice che realmente viene eseguito alla chiamata di un metodo è noto con certezza esclusivamente al runtime.


Una classe dichiara di essere sottoclasse di un'altra con la parola chiave ***extends*** dopo il nome della classe. Una classe dichiarata *final* non può essere usata come superclasse; non è possibile derivarne una sottoclasse.
```java 
package it.unipd.pdp2023;

final class App{
	private int a;
	protected int b;
	
}

//Errore di compilazione
class Foo extends App{
	private String c;
}

```

Una classe dichiarata *sealed* permette solo ad alcune classi di derivare da essa
```java 
package it.unipd.pdp2023;

sealed class App permits Foo{
	private int a;
	protected int b;
	
}

//Ok
class Foo extends App{
	private String c;
}

//Errore
class Boo extends App{

}

```
Una classe dichiarata *non-sealed* ritorna ad essere derivabile da tutti.

Una classe dichiarata ***abstract*** deve essere usatacome superclasse; non è possibile istanziarla direttamente (sono come le classi astratte in C++).

```java 
package it.unipd.pdp2023;

abstract class App{
	private int a;
	protected int b;
	
}

class Foo extends App{
	private String c;
}


App app = new App(); //Errore
App foo = new Foo(); //Ok

```

Tutti gli oggetti in Java discendono implicitamente da ***java.lang.Object***, ereditandone alcuni metodi fondamentali:
```java 
int hashCode();
boolean equals (Obejct o);
String toString();
```



### Eccezioni
La gestione degli errori in Java è implementata con un sistema di ***Tipi di Eccezione***. Le Eccezioni sono oggetti, ma vengono creati ed usati in casi particolari, e sono supportate da apposita sintassi. Tutte le eccezioni derivano dalla classe *Throwable*. Una prima suddivisione avviene fra le due sottoclassi di *Throwable*:


- *Exception*: nonostante l'erorre, il programma dovrebbe essere in grado di proseguire
- *Error*: gli errori per il quali, il programma non riesce a proseguire

Una particolare sottoclasse di Exception è *RuntimeException*: essa rappresenta ogni errore che può avvenire durante la normale valutazione diespressioni. Viene lanciata direttamente dalla JVM, e quindi nonnecessita di essere dichiarata.

Le eccezioni derivate da *RuntimeException* e *Error* sono dette ***unchecked exceptions*** e non necessitano dichiarazione nella definizione di un metodo. Tutte le altre, discendenti da *Exception* o *Throwable* direttamente, sono dette ***checked exception*** e devono essere dichiarate nella definizionedi un metodo.


La disciplina di OOP che ha ispirato questa parte di Java incoraggia la definizione di classi di eccezione legate al dominio del problema che il programma rappresenta, per esplicitare maggiormente il significato di tali condizioni di errore.