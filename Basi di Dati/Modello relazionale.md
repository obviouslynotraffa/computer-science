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
Banalmente, una tupla è una singola riga della tabella.

