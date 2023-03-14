Abbiamo diversi tipi di operazioni che possiamo fare sui linguaggi regolari:

- ***Unione***: $$L\cup M=\{w:w\in L\;oppure \;w \in M\}$$
![500](http://www2.lawrence.edu/fast/GREGGJ/CMSC515/chapt01/Regular2.png)

- ***Intersezione***: $$L\cap M=\{w:w\in L\;e \;w \in M\}$$

- ***Concatenazione***: $$L.M=\{uv: u\in L\;e \;v \in M\}$$
![500](http://www2.lawrence.edu/fast/GREGGJ/CMSC515/chapt01/Regular3.png)

- ***Complemento***: $$\bar L=\{w:w\notin L\}$$
- ***Chiusura di Kleene ( o star )***:  $$L^*=\{w_1w_2...w_k:k\geq0\;\forall w_i \in L\}$$
![500](http://www2.lawrence.edu/fast/GREGGJ/CMSC515/chapt01/Regular4.png)


Se $L$ e $M$ sono linguaggi regolari, allora anche dopo le seguenti operazioni lo saranno.

Adesso facciamo alcuni esempi, costriuamo l'automa che rappresenta l'intersezione di (a) e (b):

```mermaid
flowchart LR
startA --> id1((R0)) --1-->id1
id1 -- 0-->id2(((R1))) --0,1 -->id2

```

```mermaid
flowchart LR
startB --> id1((S0)) --0-->id1
id1 -- 1-->id2(((S1))) --0,1 -->id2

```
l'intersezione di questi due automi dovrà generare un automa che accetta solo il linguaggio che è nello stato finale di entrambi gli automi contemporaneamente. Quindi:

```mermaid
flowchart LR
start --> id1((R0,SO)) --0-->id3((R1,S0))--0-->id3
id3--1-->id4(((R1,S1)))--0,1-->id4
id1 -- 1-->id2(((R0,S1))) --0,1 -->id2 --0 -->id4

```


Alcuni esempi delle altre operazioni sono, dato $$L=\{01,010,11\}$$ $$M=\{10,001,110\}$$
$L.M=\{0110,01010,1110,01001,010001,11001,01110,010110,11110\}$ ovvero tutte le possibili combinazioni usando la prima $L$ poi $M$.

$L^*=\{\epsilon, 01,010,11,01010,0111,01011,...\}$ ovvero tutte le combinazioni possibili, ripetendo all'infinto.

