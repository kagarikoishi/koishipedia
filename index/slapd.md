# Installation d'un annuaire LDAP.
L'annuaire LDAP sous linux porte le nom claquant de *slapd*. Il faut d'ailleurs le redémarrer à CHAQUE modification (autrement il se met en croix).  
Cet utilitaire est la plus simple expression d'un logiciel de gestion LDAP, ce qui le rend simple d'utilisation.

Il faudra installer ou modifier (`sudo dpkg-reconfigure slapd`) slapd pour disposer de LDAP, ainsi qu'installer `ldap-utils `.

Il est possible d'afficher le contenu de la racine avec la commande `ldapsearch -x -b dc=lab,dc=local`

## Comment modifier une base de données LDAP ?
Pour modifier un LDAP il faut au préalable créer un fichier texte avec son éditeur favori qui devra prendre l'extension .ldif  
puis être injecté via une ligne de commande ldapadd ou ldapmodify selon le cas. Cette commande possède une tétrachiée d'options que je me dois de décrire :

### Les commandes de LDAP : ldapmodify/ldapadd

  Commande réelle (exemple) : `ldapmodify -a -x -D "cn=admin,dc=lab,dc=local" -W -f ajout.ldif`

  *Ajoute ou modifie l'annuaire avec une identification simple en tant qu'admin.lab.local, avec un formulaire de connexion avec le contenu du fichier ajout.ldif*

* ldapmodify -a ou ldapadd (ajouter une nouvelle entrée à l'annuaire)
* ldapmodify -V (imprime la version de LDAP, -VV n'affiche que cette info)
* ldapmodify -v (mode verbeux)
* ldapmodify -n (prévisualise les modifications futures sans les appliquer, utile pour vérifier ce que l'on fait)
* ldapmodify -c (les erreurs sont affichées, mais la commande continue en faisant des modifications. Par défaut -c s'interrompt à la première erreur).
* ldapmodify -f *fichier* (ajouter un fichier au lieu de lire la [sortie standard](redirection.md))
* ldapmodify -S *fichier* (les enregistrement qui devaient être modifiés ou ajoutés et qui ne l'ont pas été à cause d'une erreur sont écrits dans le fichier et le message d'erreur est rajouté en commentaire. Utilisé en conjonction de -c).
* ldapmodify -M (Met en place le contrôle Manage DSA IT, -MM le rend critique)
* ldapmodify -x (utilise l'authentification ordinaire au lieu de SASL)
* ldapmodify -D *"dn=truc,dc=test,dc=com"* (utilise le nom distingué pour lier l'instruction au répertoire LDAP)
* ldapmodify -W (affiche le formulaire de connexion et évite de devoir préciser le mor de passe dans la commande)
* ldapmodify -w (utilise passwd pour une authentification simple)
* ldapmodify -y (utilise le contenu complet d'un fichier de mots de passe comme mot de passe pour une connexion).
* ldapmodify -H *URI du LDAP* (préciser l'URI du serveur LDAP/port/hôte. Il est possible d'en ajouter plusieurs en les séparant d'une espace ou d'une virgule).
* ldapmodify -P {2|3} Vesion du protocole LDAP à utiliser.
* ldapmodify -E ou -e (**ébauche, a préciser plus tard**, recherche d'extensions).
* ldapmodify -o *timeout=25* (permet d'ajouter une option)
* ldapmodify -O (spécifie des propriétés de sécurité pour SASL)
* ldapmodify -I (mode interactif avec SASL)
* ldapmodify -Q (mode silencieux avec SASL)
* ldapmodify -N (ne pas utiliser le reverse DNS pour canoniser le nom SASL de l'hôte).
* ldapmodify -U *authcid* (Specify the authentication ID for SASL bind. The form of the ID depends on the actual SASL mechanism used).
* ldapmodify -R *realm* (Specify the realm of authentication ID for SASL bind. The form of the realm depends on the actual SASL mechanism used.)
* ldapmodify -X *authzid* (Specify the requested authorization ID for SASL bind. authzid must be one of the following formats: dn:<distinguished name> or u:<username>)
* ldapmodify -Y *mech* (Specify the SASL mechanism to be used for authentication. If it's not specified, the program wil choose the best mechanism the server knows.)
* ldapmodify -Z[Z] (Issue StartTLS (Transport Layer Security) extended operation. If you use -ZZ, the command will require the operation to be successful).  

### La structure et le fonctionnement de LDAP.

La structure d'un LDAP obéit à des règles précises qui sont d'une certaine manière similaire à une base de données (tout en n'étant pas compatible SQL).

Celle-ci contient quelques types d'attibuts :
* Le Domain Content qui contient souvent deux entrées (dc=truc,dc=local) et se réfère à un nom de domaine.
* Le Common Name qui est le nom d'un objet de LDAP (cn=chaise).
* Le Distinguished Name qui est le chemin absolu d'un objet (dn=pbalkanyo=table,dc=de,dc=dessous)
* Le Relative Distinguished Name est un chemin relatif du même objet (uid=Louison).
* Le User IDentifier qui est le nom d'utilisateur (uid=lboblet)
* Le SurName qui est un surnom (sn=loulou)
* L'Organisational Unit (ou UO) chère à Active Directory. (ou=oboulo)
* L'Organisation qui est l'entreprise (o=table)
* L'Unit qui représente le service de l'entreprise (u=larbins).
