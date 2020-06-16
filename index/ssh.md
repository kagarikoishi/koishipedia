# OpenSSH : fonctionnement.
Créer une clé publique pour OpenSSH est facile et se fait en peu d'étapes.

* `ssh-keygen` génere une paire de clés et vous proposera de les stocker automatiquement sur :
  * `C:\Users\username\.ssh\id_rsa` sous Windows
  * `~/.ssh/id_rsa` sous \*nix.

La génération de clés demandera de saisir une passphrase qui vous sera demandée (en lieu et place du mot de passe utilisateur).

Pour copier la clé, il faudra soit faire une copie automatique de la clé : `ssh-copy-id utilisateur@ip-ou-adresse-serveur` ou sinon copier la clé publique sur l'emplacement précisé dans le paragraphe précédent (sous le nom id_rsa.pub).

L'authentification ressemblera à ceci :

`PS C:\Users\Absurda> ssh -X user@10.0.1.140`  
`Enter passphrase for key 'C:\Users\Absurda/.ssh/id_rsa:`


Il faudra cependant installer un serveur SSH sur la machine distante.
