

Gli automi a stato finiti deterministico è una quintupla$$A=(Q,\Sigma,\delta, q_o, F )$$
- $Q$ è un insieme finito di stati 
- $\Sigma$ è un alfabeto finito
- $\delta$ è una funzione di transizione 
- $q_0\in \;Q$ è lo stato iniziale
- $F \subseteq \;Q$ è un insieme di stati finali 


Per comprendere meglio costruiamo un automa $A$ che accetta il linguaggio delle stringhe con 01 come sottostringa

[[image]]

Se il carattere è 1, si procede con il prossimo e si sta sempre in $q_0$, finchè non si trova uno 0, dove diventa $q_1$. Se il prossimo carattere è uno 0, sarà lo 0 dell'ipotetica sottostringa, quindi rimango in $q_1$, se invece trovo un 1, diventa un $q_2$, e rimane tale fino alla fine della stringa indipendentemente dal carattere.

In parole più formali:
Data una parola $w=w_1\;w_2\;...\;w_n$ la computazione dell'automa $A$ con input $w$ è una sequenza di stati $r_0\;r_1\;...\;r_n$ che rispetta due condizioni:
1. $r_0=q_0$ 
2. $\delta(r_i\, w_i+1)=r_i+1$ per ogni $i=0,...,n-1$ , ovvero che rispetta la funzione di transizione

Diciamo che la computazione accetta la parola $w$ se :
3. $r_n \in \;F$ , cioè la computazione termina in uno stati finale 


Un ***DFA*** (*Deterministic Finite Automaton*) $A$ accetta la parola $w$ se la computazione $w$. Formalmente il linguaggio accettato da $A$ è 
$$L(A)=\{w \in \Sigma^*\; |A\;accetta\;w\}$$
i linguaggi accettati da automi a stati finiti sono detti ***linguaggi regolari***.