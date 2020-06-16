## ACL sous Windows
* ACE : Access Control Entry : users, groupes.
* DACL : ce qui te donne les permissions par rapport aux Access
* SACL : permet de faire des audits = Onglet Audit dans les paramètres avancés d'un fichier Windows.
Dans le monde Microsoft, le refus > autres règles.

ACL : Deux types
•    Système locaux : NTFS : gestion plus fine des accès aux fichiers. (Onglet sécurité)
•    Réseaux distant : Distants peut être des adresses IP ou ports autorisés ou interdits. (Onglet partage ou sur le pare-feu).
DACL : Gère l’accès aux objets et protège les droits ACE 
SACL : Gère les logs des ACE pour reporting des droites entrées (AUDIT)
ACE : Listes de droits que l’on peut attribuer à un objet (onglet sécurité)
AUDIT : Le système écrit des messages d’audit pour chaque type de tentative d’accès dans le journal d’évènement.
HERITAGE : Droits avancés, désactiver l’héritage les sous dossiers héritent de base des droits du dossier parent.
MFT : Master File Table, table de fichiers principale du disque dur contenant les droits ACLS
NTFS : système de fichier Windows sensible à la casse évolution du fat32 
SMB :  PORT 139 et 445 protocole de partage de ressources sur des réseaux locaux Server Message BLOCK
DROITS ETENDUS : droits + droits avancés qui permettent d’affiner encore plus nos droits.
AAA : Authentification = DACL ; Autorisation = ACE ; AUDIT = SACL
Partition NTFS contient :
•    MFT
MFT contient :
•    Attributs du fichier
•    Logs
•    ACLS
