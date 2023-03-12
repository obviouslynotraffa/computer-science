> ***VCS***
> sono dei sistemi software che registrano tutte le modifiche avvenute ad un insieme di file. Permette la condivisione di file e delle modifiche. Offrono funzionalità di merging e tracciamento delle modifiche.



$\rightarrow$ Perchè un team di sviluppo dovrebbe usare un vcs?
- **Collaborare** in modo efficiente nel codice di un prodotto
- Facilita l'**individuazione** e la risoluzione di **conflitti**
- Facilita la **condivisione** di commenti e documentazione
- Tracciare ogni modifica storica del prodotto
- Facile ripristino dei file ad una versione precedente

## Tipi di VCS
Ci possono essere tre(+1) tipologie di vcs

##### Local
Sono i più vecchi e registrano ***solo la storia*** dei cambiamenti. Di solito usano un *Version Database* dove viene registrata storia di tutti i file, salvando sul disco una serie di *patch* tra una versione e l'altra. ***Non gestiscono la condivisione***.

![500](https://miro.medium.com/v2/resize:fit:800/1*4ohtoBNVHlKb21zPw-8WVQ.png)


##### Centralized
Rispetto ai locali sono meno vecchi è molto più diffusi. Gestiscono ***sia la condivisione che la storia dei file*** (la storia è gestita proprio come i local vcs e il *Version Database* è gestito in un server centrale, quindi ***un solo nodo di rottura***). Ogni sviluppatore è un client che ha nel suo spazio di lavoro solo una versione (alla volta) del codice. 

![500](https://miro.medium.com/v2/resize:fit:1000/1*BvlOIbfKQERLhvS--GkzBQ.png)

##### Distribuited
Simili ai centralized ma il database è distribuito per duplicazione in ogni nodo. Quindi, (a differenza dei centralized) ***quando il nodo centrale non è disponibile***, ***è possibile continuare a lavorare*** e registrare i cambiamenti. Hanno una migliore risoluzione dei conflitti che favorisce la collaborazione e permettono di impostare ***diversi tipi di flussi di lavoro*** che non sono possibili in sistemi centralizzati. 

![500](https://miro.medium.com/v2/resize:fit:640/format:webp/1*B63csmcab5_kbr2zSP8SLA.png)

#### Cloud-based
Il *Version Database* è gestito in un servizio cloud, quindi il codice sorgente non è nell'infrastruttura aziendale, delegando la gestione e l'installazione ad un servizio esterno. Di solito vengono forniti in aggiunta altri servizi come text editor online, strumenti visuali, issue tracking system, etc… Esempi rilevanti sono Github e GitLab.

### Terminologia
- `Commit`: ogni cambiamento di un file viene chiamato ***diff***, più diff validate fanno un commit. Un commit infatti è una nuova versione del codice. Può esistere ***sia localmente che in remoto***. L'ultimo commmit della storia viene chiamato ***head***.

- `Branch`: sono delle specie di "binari alternativi", in cui il codice viene duplicato in modo che è possibile fare lavorare su un ramo diverso da quello principale senza intaccare il codice, ma lavorandoci su comunque. Per unire due rami è possibile usando un'operazione di `merge`.

- `Pull request`: è un modo in cui vengono uniti i rami secondari e il principale. Il branch è pushato sul main senza essere stato fatto un `merge`. Prima di una pull request è possibile vedere tutti i cambiamenti fatti, discuterli, commentarli e migliorarli. Una pull request finisce quando viene chiusa o unita al ramo principale.
![](https://i0.wp.com/build5nines.com/wp-content/uploads/2018/01/GitHub-Flow.png)


### Workflow patterns
Estendendo il concetto di branch, si possono create workflows molto interesanti. Vengono usati per progetti a larga scala. Peculiarità è quella di creare diversi branch, con ruoli diversi. In tal modo è possibile lavorare su più zone del progetto senza intaccare le altre. Bisogna però ricordare che ogni tanto va fatto il merge da un nodo simil-principale, dal momento che sono versioni diverse.

![](https://expressus.io/uploads/beautiful-gitflow-workflow-diagram.png)
