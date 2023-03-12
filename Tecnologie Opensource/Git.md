Git è un software di controllo distribuito (DVCS) utilizzabile da interfaccia a riga di comando, creato  nel 2005. Nacque per essere un semplice strumento per facilitare lo sviluppo del kernel linux ed è diventato uno degli strumenti di controllo più diffusi.

Un file in GIT può essere in uno dei seguenti 3 stati:
- ***Modified***: modificato nella working directory
- ***Staged***: salva uno snapshot nella *Staging Area*
- ***Commited***: preso dalla *Staging Area* nel repository locale

![500](https://camo.githubusercontent.com/392c9afc00d23669e918cd994f4628518ed7572ae4d34bffb39eabc0dc8a756d/687474703a2f2f6769742d73636d2e636f6d2f666967757265732f3138333333666967303230312d746e2e706e67)


###### Configurazione
É richiesta una configurazione iniziale dove vengono impostati l’username e l’email da usare per ogni commit:
- *git config --global user.name "Bugs Bunny"*
- *git config --global user.email bugs@gmail.com*

É tuttavia possibile avere la lista delle tutte configurazioni con il comando:
- *git config --list*

### Comandi Git

###### Creazione del repository
- *git init* : crea una cartella nascosta .git nella cartella corrente
- *git clone "url"* : copia una repository remota nella cartella corrente e la inizializza già con git init

###### Add e Commit
- *git add nome.file* : aggiugne i file nella staging area e creazione di una Snapshot
- *git commit -m "first commit"* : commit e salvataggio di una nuova versione nel repository locale
- *git reset HEAD nome.file* : rimuove un file dalla staging area senza perdere le modifiche
- *git checkout --nome.file* : rimuove un file dalla staging area perdendo le modifiche


###### Stato e Ripristino
- *git status* : per vedere lo stato dei file nella staging area o nel workspace
- *git diff* : per vedere cos'è stato modificato ma non è ancora nella staging area
- *git log* : per vedere la lista dei cambiamenti nel repository locale


###### Branch e Merging
- *git branch name* : crea un nuovo branch
- *git branch* : per vedere la lista dei branch
- *git checkout branch.name* : per passare in un altro branch
- *git merge branch.name* : per fare un merge del branch specificato nel corrente branch


###### Repository remoto
- *git remote* : lista dei repository remoti
- *git fetch origin* : recupera i nuovi branch e le modifiche dal remoto senza aggiornare la working copy (senza fare merge)
- *git pull origin main* : recupera le ultime modifiche dal repository remoto e aggiorno la working copy (fetch and merge)
- *git push origin main* : per inviare le modifiche al repository remoto


![](https://www.junosnotes.com/wp-content/uploads/2021/07/basic-git-commands.png)
