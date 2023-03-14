Un *DFA/NFA* è un metodo per costruire una macchina che riconosce linguaggi regolari. Una espressione regolare è un modo dichiarativo per descrivere un linguaggio regolare. Le espressioni regolare sono usate tipo quando fai `Ctrl-F` per cercare una parole in un file. 


Le espressioni regolari sono costruite usando:
- un ***insieme di costanti*** di base:
	- $\epsilon$ per la stringa vuota
	- $\emptyset$ per il linguaggio vuoto
	- $a,b,c...$ per i simboli $\in \Sigma$ 

- collegati da ***operatori***:
	- $+$ per l'unione
	- $.$ per la concatenazione
	- $^*$ per la chiusura di Kleene
- raggrupati usando le ***parentesi***


Se $E$ è un espressione regolare, allora $L(E)$ è un linguaggio rappresentato da $E$. Quindi:

Con i casi **base**:
- $L(\epsilon)=\{\epsilon\}$ 
- $L(\emptyset)=\emptyset$
- $L(a)=\{a\}$

Con i casi **induttivi**:
- $L(E+F)=L(E) \cup L(F)$ 
- $L(EF)=L(E).L(F)$
- $L(E^*)=L(E)^*$



Regole di precedenza degli operatori:
1. Parentesi
2. Chiusura di Kleene
3. Concatenazione
4. Unione


La conversione tra NFA/DFA e RE, e viceversa, è sempre possibile. Infatti se $L$ è un DFA, allora  $\bar L$ avrà come stati finali tutti gli stati non finali di $L$  

Esempi:
1. Scrivere un espressione regolare per $L=\{w \in \{0,1\}^*:0\;e\;1\;alternanti\}$ 
$$(01)^*+(10)^*+1(01)^*+0(10)^*$$

