## Les commandes de base d'UNIX.
### Celles qui sont communes à tous les invités de commande de la TERRE (croyez-moi, c'est pas putaclic) : 
* cd : change directory
  * cd .. Revenir au dossier précédent
  * cd ../.. Revenir à un dossier encore en arrière
* ls (dir dans l'univers Microsoft) : lister le contenu d'un dossier. Pour les commutateurs à utiliser, lire le manuel.
* cat : miaou (lit le contenu d'un fichier texte, comme less).
* rm (et rmdir/del chez M$) : supprime un contenu.
  * rm -r : permet la suppression si le dossier n'est pas vide.
  * rm -i : demande une confirmation pour supprimer CHAQUE fichier.
  * rm -I : demande une confirmation pour supprimer qu'une fois dès qu'il y'a plus que trois fichiers.
  * (sudo) rm -rf /\* : Massacrer toute la population qui a trouvé refuge dans votre PC. Au NAPALM.
* mkdir : Créer un dossier.
* touch : Tel Dieu, vous créez quelque chose (un fichier, faut pas déconner, vous n'avez pas assez de compétences pour créer une bimbo).
* echo : Imprimer un message sur un écran. 

### Et celles qui sont exclusives au monde \*nix. 
En gros, tout le reste. Si vous avez la malchance d'avoir touché au PATH, il suffit (la plupart du temps de mettre /usr/bin/ devant).

* man : invoque le **Manuel Unix** (tm).
* --help (-h ne correspond pas forcément à help) Liste des commutateurs qui existent sur une commande.
#### Mise à jour.
* apt/yum/aur/aptitude/snap : Gestionnaire de logiciel (software repository de $DISTRIBUTION. Attention, APT n'a pas les pouvoirs de super-vache !
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
	
