Proprio come avviene nei compilatori di altri linguaggi, non c'è nessuna garanzia che l'ordine di esecuzione delle istruzioni sia lo stesso del codice. Infatti il compilatore si prende grandi libertà su come organizzare, riscrivere e modificare il sorgente iniziale.

## Dichiarazioni
Una istruzione può essere una dichiarazione di un nome e del suo tipo. Può essere dichiatata una vaiabile, una classe che sono dette locali rispetto al blocco che le contiene.

Una variabile viene dichiarata indicando il tipo, nome ed eventualmente un valore a cui inizializzarla. Usando la parola chiave `var`, si lascia al compilatore dedurre il suo tipo. Indicando una lista vuota di parametri tipo <>, anche questa sarà dedotta dal compilatore (sempre se possibile).

```java
int i=1;
var b=java.util.List.of(1,2);
Foo a = new Foo("bar");
int[] r = new int[] {1,2,3};
```

Bisogna stare attenti al blocco di delle` {}` che contiene il codice, perché potrebbe portare a equivoci indesiderati. Nell'esempio qui sotto, `Local` non hanno lo stesso tipo.

```java
class Global{
	class AnotherLocal{
		void bar(){
			class Local{}
			Local l= new Local();
		}
	}
	
	{
	class Local {}
	Local a = new Local();
	}	
}
```



## Espressioni
Una istruzione può consistere in una espressione, cioè una sintassi che produce un valore, anche se questo non viene usato.
Le espressioni seguono abbastanza da vicino le regole di precedenza, struttura e semantica della maggior parte dei linguaggi.

Le espressioni possono contenere valori letterali per i principali tipi primitivi.

| Tipo      | Esempi                         |
| --------- | ------------------------------ |
| Interi    | 12, 45L, Oxf, 077, 0b1111_0000 |
| Decimali  | 0.0, 3.14f, 1.6e5,             |
| Booleani  | true, flase                    |
| Caratteri | "a", "€"                       |
| Stringhe  | "abdce", "cinese e arabo"      | 

I tipi interi possono essere anche in binario, ottale ed esadecimale se serve.

```java
byte a = (byte)0xff;
short s = (short)12800;
```
Non è possibile indicare una costante di larghezza byte o short senza operatore di cast



Le costanti di tipo `String` hanno un trattamento speciale da parte del compilatore:
- sono oggetti `String`, senza bisogno dell'operatore `new`
- possono essere su più righe (molto utile per le query in Sql)
- sono immutabili

```java
String square = """
	SATOR
	AREPO
	TENET
	OPERA
	ROTAS""";
```

La parola chiave `null` indica il valore nullo, ovvero il riferimento che non punta a nessun oggetto.
E' l'unico tipo dell'elemento del tipo `null`, che non ha nome, non si uò esprimere e può sempre essere convertito in ogni altro oggetto.


## Assegnamento
L'assegnamento `=` è un operatore, quindi l'assegnazione è una espressione e quindi una istruzione.
Il valore dell'espressione è lo stesso assegnato alla variabile.
```java
int x;
x=(int)4.6; //tronca a 4

int k=1;
k+=(k=4)*(k+2) // k=25 ma se scrivi cosi meriti la morte
```



## Chiamata di un metodo
L'esecuzione della chiamata di un metodo è una espressione come le altre. Se non ritorna un valore, è una istruzione a se stante
```java
System.out.printIn("k==" + k + "and a[0]=="+ a[0]);

int time=System.currentTimeMillis();
```
Notare che la concatenzaione delle stringe con i valori avviene tramite l'operatore `+` .


## Creazione di un oggetto
La creazione di un oggetto è la chiamata ad un metodo che ritorna il nuovo oggetto. E' quindi un espressione.
```java
StringBuffer buf= new StringBuffer("Text");
buf.toString().toUpperCase();
```






## This e Super
Le parole chiave `this` e `super` hanno un significato particolare.
- `this`: permette di indicare l'istanza corrente durante l'esecuzione del metodo. Può essere utile per risolvere ambiuìguità di denominazione o per rendere più esplicito il significato dell'espressione.
```java
class Foo{
	public final int idx;
	public final String title;
	
	public Foo(int idx, String title){
		this.idx=idx;
		this.title=title;
	}
}
```

- `super`: indica l'oggetto padre della gerarchia di ereditarietà. Permette di controllare il passaggio di argomenti al costruttore della classe padre, all'interno del costruttore della classe figlio.
```java
class A{
	public final int a;
	public A(int a) {this.a=a;}
}

class B extends A{
	public final int b;
	pubic B(int a,  int b){
		super(a);
			this.b=b;
	}
}
```


## Lambda expression
Una delle maggiori innovazioni è stata l'introduzione delle lambda expressions, che permettono di scrive codice molto snello. Sono simile a quelle del C++. La sintassi è la seguente
```java
( < lista parametri > ) -> istruzione
```
Il compilatore individua il tipo che è atteso nell'espressione in cui la lambda si trova. Il risultato è un' istanza di un oggetto che implementa tale tipo, con il comportamento dell'istruzione.

```java
() -> 42
() -> {return 42;}
() -> {System.gc();}

(int x) -> {return x+1;}
x->x+1

(int x, int y) -> x+y

```

***ATTENZIONE***: le lambda expression ***non*** rendono java un linguaggio funzionale.

Non hanno un tipo proprio, è solo una sintassi breve per casi d'uso comuni. Il compilatore sostituisce il codice necessario per ottenere lo stesso risultato.



## Condizionali
In Java i costrutti condizionali sono istruzionali, non espressioni. Questo significa che eseguono blocchi di codice separato dalla virgola del valore della condizione.

- `If`, `else`: l'istruzione ha la stessa struttura del C. La condizione deve essere booleana.
- `switch`: la selezione fra più valori è anch'essa mutuata dal C, con qualche estensione
```java
enum Days{LUN, MAR, MER, GIO, VEN, SAB, DOM;}
Days day=...;

switch(day){
	case LUN:
		System.out.printIn("Inizio settimana");
	break;
	
	case SAT, DOM
		System.out.printIn("Fine settimana");
	break;
	
	default
		System.out.printIn("Nel mezzo");
	break;
}
```

A partire da Java 14, gli `switch` sono in grado di ritorna un valore. La forma esteriore è molto simile, ma ci sono alcune fondamentali differenze.

Sono disponibili due tipi di versioni:
```java
enum Days{LUN, MAR, MER, GIO, VEN, SAB, DOM;}
Days day=...;

String weekPart=switch(day){
	case LUN:
		System.out.printIn("Inizio");
		yield "Inizio settimana";
		
	case SAT, DOM
		System.out.printIn("Fine");
		yield "Weekend"
		
	default
		yiedl "Nel mezzo";
}
```

La parola chiave `yield` è una specie di return, può essere preceduto da alcune istruzioni, o incluso in un blocco, o isolato. Non c'è fall-through. L'elenco dei casi deve essere esaustivo.

Oppure c'è la versione con le lambda expression
```java
enum Days{LUN, MAR, MER, GIO, VEN, SAB, DOM;}
Days day=...;

String weekPart=switch(day){
	case LUN -> "Inizio settimana";	
	case SAT, DOM -> "Weekend"	
	default ->{
		yiedl "Nel mezzo";}
}
```


## Iterazioni
Anche le iterazioni sono ispirate, se non identiche, a quelle del C

###### While
```java
int i=0;
int sum=0;
while(i<100){
	sum+=i++;
}
```

###### Do-While
```java
boolean condizione;
do{
	//cosa da fare
}while(condizione)
```
Il ciclo fa sempre al meno una iterazione, poichè la condizione per ciclare è posta alla fine del blocco di codice.


###### For
```java
for(int i=0; i<n;i++){
	//fai cose
}
```


Ci sono poi delle parole chiavi aggiuntive che ci permettono di manipolare meglio i cicli:
- `break`: interrompe immediatemente il ciclo più interno in corso
- `continue`: interrompe l'iterazione in corso, per passare a quella successiva



## Eccezioni

##### Try-Catch
Se un metodo dichiara la possibilità di lanciare un certo tipo di ecezzione, il codice chiamante è obbligato dal compilatore  a dichiarare la stessa eccezione oppure a gestirla all'interno di un blocco `try-catch`.

```java
class Foo extends Exception {}

class Foo {
	void a() throws FooException {return;}
	void b() throws BarException {
		try {
			a();
		} catch (FooException e){
			e.printStackTrace();
		} finally {
			System.out.printIn("Always");
		}
	}
}
```
Il blocco di codice introdotto nell'istruzione `try` viene eseguito, se viene lanciata un'eccezione il primo blocco `catch` adatto viene eseguito (occhio a dichiarare i catch dal grado di specificità del tipo maggiore fino al minore). Il blocco `finally` viene eseguito comunque.


##### Try-with-resources
Un'altra clausola dell'istruzione try, detta `try-with-resources`, permette di dichiarare delle variabili. Queste devono implementare l'interfaccia `AutoClosable`, e verranno automaticamente e con certezza chiuese. I `catch` e `finally` sono opzioniali.



##### Throw
Per lanciare eccezioni destinate ad essere catturate da una istruzione `try`, è disponibile l'istruzione ***throw***. Richiede un oggetto discendente da `Exception` che viene lanciato come se fosse avvenuto un errore.