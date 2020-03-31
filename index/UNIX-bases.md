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
* touch : Tel Dieu, vous créez quelque chose (un fichier, faut pas déconner, vous n'avez pas assez de compétence pour créer une bimbo).
* echo : Imprimer un message sur un écran. 

### Et celles qui sont exclusives au monde *nix. 
En gros, tout le reste.
* man : invoque le **Manuel Unix** (tm).
* --help (-h ne correspond pas forcément à help) Liste des commutateurs qui existent sur une commande.
* apt/yum/aur/aptitude/snap : Gestionnaire de logiciel (software repository de $DISTRIBUTION. Attention, APT n'a pas les pouvoirs de super-vache !
* *apt-get* update : mise à jour du gest. de log. favori.
* *apt-get* upgrade : mise à jour des paquets de votre \*nix.
* *apt-get* install *logiciel* : Installer un logiciel.
