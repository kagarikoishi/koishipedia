# Le Serveur Windows - Windows 2016
Windows Server est un système d'exploitation qui consiste principalement à appuyer sur Suivant. 
Malgré ce défaut qui le rend particulièrement inintéressant, il est possible de ne plus sentir sa souris au bout de quelques heures et de produire une connerie qui risque de le rendre instable.

### Les conneries 

* [Active Directory (lien récursif)](active-directory-bases.md)
* Seveur DNS et DHCP (ne mérite pas de page supplémentaire)

Le DHCP se configure simplement, mais il ne faut pas oublier de l'autoriser (C'est rappelé dans la console DHCP, d'ailleurs) et dans le cas où il y a deux serveurs il faut faire un basculement (clic droit quelque part).

Le DNS est un peu plus complexe. Il faudra modifier les enregistrements pour faire du DNS redondant (sauf AD ?) en ajoutant le serveur redondant et en lui déterminant un rôle (en tant que zone secondaire/stub par ex). Le serveur redondant ne pourra être SOA (qui est unique et peut écrire sur les autres DNS de la zone). Le SOA soit aussi être hors-ligne pour éviter tout risque d'attaque.
* [Serveur de déploiement](microsoft-deployment-services) (Microsoft Deployment Service)
* Serveur de déploiement de mises à jour (WSUS).
* Sauvegarder et faire une backup du Serveur.  
* Serveur HTTP Intranet (Microsoft IIS)
C'est assez simple et peu utile. 
* Powershell (aka. Comment trouver des scripts pour automatiser la création de nouveaux utilisateurs -- et les désactiver pour ne pas perdre son emploi).
* Gestion de certificats.
* Sans oublier [les bonnes pratiques](pratiques).

_________________

