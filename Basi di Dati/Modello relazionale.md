il modello relazionale si basa sul concetto matematico di relazione. Le rappresenteremo per mezzo delle tabelle.

Una relazione è un'insieme di attributi (colonne) tali che
$$R=\{A_1,A_2,...,A_3\}$$
ogniuno appartenente a un dominio $Dom(A_i)$ 


| string | string | int | int |
| ------ | ------ | --- | --- |
| Juve   | Lazio  | 3   | 1   |
| Lazio  | Milan  | 2   | 0   |
| Juve   | Roma   | 0   | 2   |
| Roma   | Milan  | 0   | 1   |

- l'ordinamento tra le righe è irrilevante
- l'ordinamento tra le colonne è irrilevante
- le righe son tutte diverse tra loro
- le intestazioni delle colonne sono diverse tra loro
- i valori di ogni colonna sono definiti su domini omogenei


### Istanze
Data la relazione $R(A_1,...,A_n)$. Sia $V_i$ il dominio dei valori dell'attributo $A_i$ .

La tupla r è una funzione :
$$r:\{A_1,...,A_n\}\rightarrow(V_1\cup...\cup V_n)$$
Banalmente, una tupla è una singola riga della tabella. Una istanza è un'insieme di tuple.


### Strutture nidificate
Per evitare ridondanza nelle tabelle, che non è mai buona cosa, perché viene occupato spazio per un'informazione che già c'è e si può rischiare l'incoerenza, si possono utilizzare delle strutture nidificate.
![](https://www.researchgate.net/publication/267239986/figure/fig12/AS:669488701771784@1536629953500/Example-of-Nested-Tables-In-Figure-4-NESTED-TABLE-A-represents-the-attribute.ppm)


>***NULL***
>Non sempre sono tutte le informazioni sono disponibili, per questo, viene usato un ***valore nullo***, che denota l'assenza di un valore del dominio: ***ma non è un valore del dominio !*** Si possono imporre restrizioni sulla presenza di valori nulli.



### Vincoli di integrità 
Sono delle proprietà soddisfatte dalle istanze corrette delle basi di dati. Un vincolo è una funzione booleana: quindi per ogni istanza ritorna true o false.
Abbiamo due casi:
- I vincoli **supportati** nativamente dai DBMS
- I vincoli **non supportati** nativamente

I vincoli a loro volta di suddividono in :
##### Vincoli intrarelazionali
- Vincoli di ***dominio e tupla***: esprimono condizioni sui valori di ciascuna tupla, indipendentemente dalle altre tuple(ad esempio la somma di due attributi deve essere uguale al terzo). Di fatto un vincolo di dominio è un caso particolare di vincolo di tupla su un solo attributo.(voto >=18 e <=30). 
- Vincoli di **chiave**: non ci posssono essere tuple che hanno la stessa chiave.

##### Vincoli interrelazionali
Sono informazioni che sono in relazioni diverse, ma collegate attraverso valori comuni. Le correlazioni devono essere coerenti. Uno o più attributi è collegato/i con una chiave primaria di una seconda relazione. L'attributo che non è chiave primaria in una relazione, ma in un'altra viene detta ***chiava esterna***.



### Chiave e superchiave

>***SUPERCHIAVE***
>Un insieme $K=\{k_1,...,k_n\}$ di attributi di una relazione $R$ è ***superchiave*** se non ci sono due tuple in $R$ con gli stessi valori per tutti gli attributi di $K$. Formalmente per ogni coppia di tuple, se sono diverse, allora anche i loro attributi lo sono. Una superchiave idetifica le tuple in una relazione.


>***CHIAVE***
>É semplicemente una superchiave minimale, cioè una superchiave $K=\{k_1,...,k_n\}$ è chiave se per ogni $k_i \in K$ non è superchiave.

Esempi di chiave possono essere:
- matricola: è superchiave, contiene solo un attributo, quindi è minimale
- Cognome, Nome e Data di nascita: è superchiave, è minimale

Una chiave identifica una tupla di una relazione, quindi può essere usata per essere referenziata da un‘altra tabella.

![500](https://www.andreaminini.com/data/andreaminini/vincolo-integrita-referenziale-database-esempio-1.gif)


### Chiavi primarie
Gli attributi delle chiavi non possono avere valori nulli. Questo perché, in presenza di valori nulli nelle chiavi, non si possono identificare le tuple e di realizzare facilmente riferimente e relazioni. Le chiavi che non possono avere valori nulli sono chiamate Chiavi primarie, è c'è esattamente una chiave primaria per relazione.

