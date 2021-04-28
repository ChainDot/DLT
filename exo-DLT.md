# Exercices Distributed Ledger Technology

Vous devrez push les réponses aux questions suivantes dans un fichier `Markdown` qui sera accessible sur votre repository github

Vous devrez fournir le lien vers ce fichier dans le formulaire de rendus d'exercices suivant: https://forms.gle/Ks8DYYR1LqQ6UD8S7

- Lire le livre blanc: https://bitcoin.org/bitcoin.pdf, cherchez une version française si vous avez du mal avec l'anglais. (Mais dans ce cas vous risquez d'avoir du mal avec la Blockchain tout court).

- Un arbre de merkle nécessite une paire de hashes pour produire un nouveau hash parent. Il faut donc a absolument que le nombre de transactions qui produiront le `Merkle root` soit pair.  
  Comment est géré le cas ou le nombre de transactions dans le Block à valider est impair pour générer un `Merlke root` ?

  If the block has an odd number of transactions, the hash of the last one is duplicated and added to itself.

https://changelly.com/blog/merkle-tree-explain/

- Dans le réseau bitcoin, Comment un nouveau noeud arrive t'il à retrouver ses pairs et ainsi rejoindre le réseau ?
  Expliquer le processus avec vos propres mots.

  Un nouveau noeud doit trouver un noeud déjà existant pour pouvoir participer.

Le nouveau noeud doit établir une connexion TCP, habituellement le port 8333 (qui est le port généralement utilisé par BC bitcoin), ou un port alternatif s’ il est prévu.

Lors de la connexion, le nœud va transmettre un message contenant des informations permettant son identification.

- Pouvez vous nommer au moins une personne qui a ou aurait pu influencer directement ou indirectement la création de Bitcoin par ses travaux (une personne qui n'a pas été nommée dans le cours)?

Nick Szabo a proposé le projet Bit gold en 1998 un premier essai à la création d’une monnaie digitale décentralisée, il est également un pionner sur le concept de smart contracts proposé en 1994.

- Avec vos propres recherches et grâce aux compétences acquises en cours pouvez vous expliquer comment une Blockchain crée un lien entre ses différents Blocks?

Dans une blockchain, le dernier block possède le hash du block header précédent, il n’est donc pas possible de modifier les txs d’un block sans modifier le hash.

- Quelle structure de données informatique peut représenter le mieux cette chaine de Block: https://en.wikipedia.org/wiki/List_of_data_structures ?

Une linked list inversée est ce qui représente le mieux une chaîne de block. Quand un nouveau block est créé, il contient la data du block ainsi qu’un pointeur vers le block précédent.

- Si je souhaite modifier une transaction de 10 bitcoin que j'ai effectué il y a 6 mois en une transaction de 1 Bitcoin, que dois je modifier dans la Blockchain et que dois je mettre en oeuvre pour que cette modification persiste ?  
  Est ce possible selon vous ?

Chaque block dans une blockchain valide toutes les transactions d’un block et dans l’ordre ou elles ont été validées.

Cela est possible, car le block header contient le hash de toutes les transactions du bloc.
Modifier une transaction dans un block modifiera le hash de toutes les transactions ce qui modifiera le hash du block header. Ce qui rendra le proof of work du hash du block header invalide. Donc, pour pouvoir modifier la transaction, il faudrait refaire le bloc avec la nouvelle transaction et reminer le bloc.
De plus, comme le block header contient le hash du block précèdent. Il faudra également reminer tous les blocks qui suivent et qui contiennent la transaction modifiée.
Et enfin modifier ainsi un bloc, va créer un fork de cette blockchain. Et pour être accepté par le reste du réseau, le fork devra avoir plus de travail cumulé que la blockchain actuelle. Ce qui équivaut à avoir une longueur de blockchain supérieur a la version actuelle.
Pour finir, modifier des transactions qui sont déjà dans un block validé requiert le reminage du block, ce qui requiert une puissance de calcul énorme et donc impossible dû au coup prohibitif du changement et de la puisssance de calcul nécessaire.
