## Les commandes de base d'UNIX.
### Celles qui sont communes à tous les invités de commande de la TERRE (croyez-moi, c'est pas putaclic) : 
* cd : change directory
  * cd .. Revenir au dossier précédent
  * cd ../.. Revenir à un dossier encore en arrière
* ls (dir dans l'univers Microsoft) : lister le contenu d'un dossier. Pour les commutateurs à utiliser, lire le manuel. **namei liste seulement les noms**
* *cat : miaou (lit le contenu d'un fichier texte, comme less). Unix uniquement*.
* cp : copier.
* mv : déplacer un fichier / renommer un fichier (`mv fichier texte.txt` changera le nom de fichier en texte.txt).
* rm (et rmdir/del chez M$) : supprime un contenu.
  * rm -r : permet la suppression si le dossier n'est pas vide.
  * rm -i : demande une confirmation pour supprimer CHAQUE fichier.
  * rm -I : demande une confirmation pour supprimer qu'une fois dès qu'il y'a plus que trois fichiers.
  * (sudo) rm -rf /\* : Massacrer toute la population qui a trouvé refuge dans votre PC. Au NAPALM.
* mkdir : Créer un dossier.
* touch : Tel Dieu, vous créez quelque chose (un fichier vide, faut pas déconner, vous n'avez pas assez de compétences pour créer une bimbo).
* echo : Imprimer un message sur un écran. 
* more : Permet de faire défiler le texte lentement, **lurk moar**.

### Et celles qui sont exclusives au monde \*nix. 
En gros, tout le reste. Si vous avez la malchance d'avoir touché au PATH (avoir créé des alias foireux ou modifié une variable d'environnement), il suffit la plupart du temps de mettre /usr/bin/ devant.

* man : invoque le **Manuel Unix** (tm).
* --help (-h ne correspond pas forcément à help) Liste des commutateurs qui existent sur une commande.  

* *Ctrl+Z* : Interrompre une tâche en cours.
	* fg : Reprendre la tâche en avant-plan (le terminal utilisé est bloqué tant que l'appliacation tourne).
	* bg : Reprendre la tâche en arrière-plan (permet d'utiliser le terminal).
* *Ctrl+C* : Tue le processus actif en avant-plan (en mode terminal).
	* kill *13451* : Tue la tâche qui a le PID 13451 (voir `ps` pour obtenir le PID).
	* kill *%6*    : Tue la tâche qui a le job n°6 (noté `[6] bash` quand interrompue).
	* pthread_kill : Variante qui permet de tuer un thread (sous-processus)/
	

#### Mise à jour.
* apt/yum/aur/aptitude/snap : Gestionnaire de logiciel (software repository de $TonLinux). Attention, APT n'a pas les pouvoirs de super-vache !
  * *apt-get* update : mise à jour du gest. de log. favori.
  * *apt-get* upgrade : mise à jour des paquets de votre \*nix.
  * *apt-get* install *logiciel* : Installer un logiciel.
  * *apt-get* autoremove : supprime les paquets inutiles.
#### Réseau.
* ip : remplace **ifconfig** et les autres **net-tools** (arp...) de Linux depuis quelques années. Il est similaire à ce que l'on retrouve chez (Cisco)[cisco.md] et peut s'abréger pareillement. 
	* ip a(ddress) : Affiche toutes les cartes réseau du PC.
	* ip r(oute) : Affiche la table de routage
		* ip route add 172.16.0.0/16 via 172.31.255.254 : Ajouter une route **via** une passerelle
		* ip route add 172.16.0.0/16 dev eth0 : Ajouter une route par le biais d'une carte réseau (**dev**ice).
		* ip route del 172.16.0.0/16 dev eth0 : supprimer une route (idem à add).
	* ip l(ink) : Montre les protocoles de niveau 2 (MAC, MTU...) et peut fermer une carte réseau.
		* ip link show *eth0* : Montre l'adresse MAC d'une carte réseau (utile pour (pfSense)[pfsense.md]).
		* ip link set dev *eth0* down/up : éteint ou allume une carte réseau.
		* ip link set dev *eth0* address *AA:BB:CC:DD:EE:FF* : changer l'adresse MAC d'une carte réseau, pas besoin d'une application pour ça contrairement à Windows ! 
	* ip n(eigh) : table ARP (*neighbour == voisin*).
	* *~ à suivre.
* wget : récupérer du contenu depuis Internet, pratique car continue de télécharger même déconnecté de sa session.
* w3m / lynx : navigateurs web en mode texte (utiles le jour où le serveur graphique du PC plante...
#### Exécution et scripts
* chmod : Permet de modifier les ***ACL*** (Access-List Control) et aussi rendre exécutable un script `chmod +x bash.sh`.
* ./*script.sh* ou bash *script.sh* : Permet de lancer un script.
* nano/vi/emacs *script.sh* : Rédiger dans le fichier via son éditeur de texte favori.
* `#!/bin/bash` : She-bang. Tous les scripts bash doivent commencer par cela.
#### Création d'une variable.
* `export PATH=${PATH}:/chemin/du/fichier:un/autre/fichier` : Ajoute des chemins à ajouter dans la variable $PATH. Chaque chemin doit être séparé par : 
* alias '*update*'='sudo apt-get update' : crée un alias pour une commande. A noter que cela ne marche que dans le teminal courant tant que ce n'est pas enregistré dans ~/.bashrc (comme les modifications de la variable $PATH).
#### D'autres commandes.
	
