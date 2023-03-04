
I numeri si possono rappresentare con basi diverse. La base più comune per noi umane è la 10 dato che contiamo con 10 dita delle mani, ma per le macchine usiamo la base 2.

La base del calcolatore corrisponde al fatto che l'unità fondamentale di memoria può assumere due stati fisici distinti:
- parte intera $\in \mathbb{N}$ 
- parte frazionata $\in [0,1]$ 

la parte frazionata in genere ha infinite cifre e tecnicamente è una serie a termini positivi ***convergente***. Facciamo un esempio in base 10:

$$x=+1278.3405...$$
$$= (+1)(1278+0.3405...)$$
$$=(+1)(1\cdot 10^3+2 \cdot 10^2+7\cdot 10^1+8\cdot10^0+3\cdot 10^{-1}...)$$
per far vedere che la serie della parte frazionaria è convergente e quindi rappresenta effettivamente un numero $\in [0,1]$ si usa il criterio del confronto per serie e termini non negativi. Infatti

$$c_{-j}\;b^{-j}\leq (b-1)b^{-j}$$
$$0\leq c_{-j}\leq b-1$$
$$\sum_{j=1}^\infty c_{-j}\;b^{-j}\leq (b-1) \sum_{j-1}^\infty b_{-j}$$
e quindi tutto si riduce alla serie geometrica di ragione $a=b^{-1}=\frac{1}{b}<1$ perché $b>1$. A questo punto conviene ricordarci le proprietà di somma e delle serie geometriche. 

Chiamiamo $S_n=\sum_{j=0}^{n}a^j$  dove $a \in \mathbb{R}$ 

$$S_n=1+a+a^2+...+a^n$$
$$aS_n=a+a^2+...+a^{n+1}$$
$$aS_n-S_n=(a-1)S_n=a^{n+1}-1$$
$$S_n=\frac{(a^{n+1}-1)}{(a-1)}\;\;\;\;\;\;per\;a\neq1$$

Ora $a^{n+1}$ diverge per $|a|>1$ mentre $a^{n+1}\rightarrow 0$, $n \rightarrow \infty$ per $|a|<1$, allora per $|a|<1$ 
$$\sum_{j=0}^{\infty}a^{j}=\lim_{n=\infty} S_n=\frac{1}{1-a}, \;\;|a|<1$$


Nel nostro caso $a=b^{-1}<1$ allora la serie della parte frazionaria è maggiorata da una serie geometrica convergente (a meno del fattore $b-1$) e quindi converge.

$$\sum_{j=1}^{\infty} c_{-j}\;b^{-j} \leq (b-1)\cdot \sum_{j=1}^{\infty}b^{-j}$$
(l'indice parte da $j=1$ e non da $j=0$ ma questo non cambia niente per la convergenza)


Per vedere che la parte frazionaria sta in $[0,1]$, osserviamo che se tutte le cifre dopo la virgola sono uguali alla cifra massima, la parte frazionaria è 1. In base 10 sarebbe:
$$(0.\overline{999}...)=\sum_{j=1}^{\infty}9\cdot 10^{-j}=9\;\sum_{j=1}^{\infty}10^{-j}= 9\;\cdot (\frac{1}{1-\frac{1}{10}}-1)=9\;\cdot (\frac{10}{9})-1= 9\cdot \frac{1}{9}=1 $$



Facciamo alcune osservazioni fondamentali:
- ***i numeri irrazionali hanno parte razionale infinita in qualsiasi base***. Il motivo è che i numeri  con parte infinita in una base sono necessariamente numeri razionali, perché è somma (a meno del segno) della parte intera che è un numero naturale e di una combinazione lineare.
- i numeri razionali possono avere una parte frazionaria finito o infinita ***a seconda della base.***


A questo punto possiamo affrontare la prima questione fondamentale: siccome per rappresentare un numero reale avremo a disposizione una quantità finita di cifre, **che ERRORE si fa approssimando un numero real troncando la parte frazionaria ad $n$ cifre**?


Gli oggetti che si usano non sono praticamente mai perfetti, ma approssimati a meno di un certo errore. La cosa importante è stimare questi errori e studiare il loro effetto nei calcoli, non propagando gli errori.


Concentriamoci ora sull'errore di troncamento ad n cifre:
