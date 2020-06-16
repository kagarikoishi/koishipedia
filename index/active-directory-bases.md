# Les bases d'Active Directory

Un article de Koishipédia   

Cet article est une partie à propos du fonctionnement de [Windows Server](windows-server-bases).   
Pour la partie Linux d'Active Directory c'est la partie [ldap/Active Directory](slapd-ad.md) qu'il faudra consulter.  
Pour la partie Azure Active Directory c'est dans la page sur [Microsoft Azure](azure.md).  
Cette page décrit le fonctionnement théorique d'AD et ne rentre pas dans les détails Powershell [qui est ici](powershell/ad.md)  

Sommaire :   

1. Présentation.
2. Les différents annuaires Active Directory
3. Le rôle DNS qui est enchâssé dans AD.
4. Les rôles FSMO
5. La gestion des groupes utilisateurs (GSG)
6. La gestion des politiques d'utilisation (GPO)

## Présentation

Active Directory est un ensemble d'annuaires crée par Microsoft qui correspond au standard LDAP x500 et inclut aussi un pseudo-PKI et un serveur DNS.  

L'Active Directory permet de créer un domaine, des groupes de sécurité (GSG) et ainsi de gérer un parc informatique de taille considérable.   

Il s'agit très certainement du dispositif Microsoft le plus fiable qui soit, ce qui est crucial du fait de son rôle.   
Active Directory a un certain nombre de composants que l'on retrouve dans sa version la plus répandue, l'AD-DS (Active Directory - Domain Controller), qui contient :

* Un serveur DNS (qui ne doit pas être installé préalablement à AD) et qui contient des pointeurs spécifiques à AD (SRV par exemple).  
* Un service Kerberos qui est une pseudo-infrastructure à clé publique (PKI) ayant pour but de sécuriser la communication.  
* Les rôles FSMO (dits *maîtres d'opérations*) qui sont là pour attribuer un maître à des rôles (Windows Server) qui en nécessitent (Active Directory étant capable de se répliquer et d'être piloté par n'importe lequel des contrôleurs de domaine AD).
* Des groupes d'utilisateurs ou groupe de sécurité, qui existent en quelque sorte dans les éditions client de Windows 10 (où ils ne peuvent pas être créés), tel que le groupe administrateur. AD permet de créer des groupes, qui sont souvent dans des Unités d'Organisation.
* Enfin nous avons les non moins importantes GPO, qui sont présentes dans toutes les versions de Windows (via gpedit.msc) et permettent de restreindre l'utilisateur de l'ordinateur.

## Les annuaires d'Active Directory

Active Directory existe en plusieurs déclinaisons, qui permettent d'avoir des rôles spécialisés :

> *Ebauche à combler*

* AD-DS : Contrôleur de domaine pour Active Directory, l'annuaire le plus répandu de la liste.
* AD-LDS : Similaire au précédent, il est plus léger et surtout en lecture seule. Il n'est qu'un annuaire.
* AD-RMS : Permet de gérer les permissions d'accès à part d'un AD-DS et de protéger les documents ainsi qu'une gestion centralisée des mots de passe. Les fichiers partagés deviennent illisibles en dehors du domaine.
* AD-CS : Gestion des certificats pour les serveurs du domaine (cetrificats SSL...) et sert de PKI. Il peut être autonome (bien que peu utile).
* AD-FS : Service de fédération d'un ensemble de contrôleurs.

## Le rôle DNS d'Active Directory


Active Directory est fourni avec un DNS qui se sépare en deux parties : "mondomaine.local" et "\_msdcs" qui est endémique à AD et où s'installe le contenu nécessaire pour communiquer en tant que contrôleur de domaine.  Le DNS AD ne contient pas par défaut de zone de résolution inverse et est embarqué (comme presque tout le reste) dans `C:\WINDOWS\NTDS.dit`

## Les rôles FSMO.
*Commande qui montre qui a le rôle FSMO sur un domaine AD*

    netdom query FSMO

*Une page qui montre le fonctionnement précis des rôles FSMO :* [*lien externe*](https://matteu31.wordpress.com/2017/05/09/ad-les-roles-fsmo-et-leur-fonction/)

Dits maîtres d'opérations, ils permettent de désigner un contôleur de domaine AD qui devient maître d'un secteur en particulier (tous les rôles ne peuvent pas être répliqués sans maître).  

Ce sont ceux-ci :
* Maître d’attribution des noms de domaine : Gère l'attirbutions de noms de domaine. AKA DNS-SOA.
* Contrôleur de schéma : Est le maître du schéma LDAP qui lie les serveurs de la forêt Active Directory.
* Maître RID : Maître des identifiants utilisateurs relatifs au domaine (RID, par opposition à l'identifiant SID) Cet identifiant est connu sous [ldap](slapd.md) comme UID et GID (User et Group IDentifier)
* Maître d’infrastructure : C'est le contrôleur qui est en charge de lier les utilisateurs et groupes ainsi que les objets Active Directory (lien entre les SID et GUID).
* Émulateur PDC : Primary Domain Controller, maître choisi pour la **réplication des mots de passe et le serveur de temps**. C'est aussi un émulateur de maître de domaine pour Microsoft NT 4.0 (W95/W98).
* La gestion des maîtres d’opération :

## Les Group Policies (GPO) et gestion d'utilisateurs sous AD :
*idnetiques à ce que l'on retrouve sur la console gpedit.msc*  

GPO :  Stratégies de groupe, fonctions permettant une gestion centralisée afin de restreindre les actions et les risques potentiels des objets (utilisateurs et ordinateurs).
Exemples : 
•    Le verrouillage du panneau de configuration,
•    La restriction de l’accès à certains dossiers,
•    La désactivation de l’utilisation de certains exécutables,
Les stratégies de groupe peuvent contrôler :
•    Clés de registre
•    La sécurité NTFS
•    La politique de sécurité et d’audit
•    L’installation de logiciel
•    Les scripts de connexion et de déconnexion
•    La redirection des dossiers
•    Les paramètres d’Internet Explorer

Registry Local : Est une base de donnée utilisée par le système d’exploitions. Contient les données de configuration du système d’exploitation et des autres logiciels désirant s’en servir.
Les GPO modifient la base de registre :
HKEY CURRENT USER : Gère les configurations des utilisateurs en cours
HKEY LOCAL MACHINE :  Contient les informations qui sont générales à tous les utilisateurs de l’ordinateur

c:\Windows\sysvol est utilisé par les GPO, et utilise les ports SMB pour se propager (TCP/UDP 137-139, 445)

Les GPO se propagent de l'ordinateur local, puis au site, au domaine et enfin au niveau de l'OU, et s'appliquent en général au bout de 90 mn (sauf si une déconnexion ou un redémarrage est nécessaire...) pour forcer une mise à jour, il est possible de faire une MàJ forcée via `gpupdate /force`. `gpresult` permet d'imprimer les GPO activées.

### Astuces
CMD, en tant qu'admin

    > redirusr "OU=GRETA,DC=TARS,DC=priv"  

redirige les utilisateurs crées postérieurement dans l'OU GRETA de son AD sans avoir a utiliser la console MMC *Utilisateurs et Ordinateurs AD*.

    > redircmp "OU=GRETA,DC=TARS,DC=priv"

idem, pour un ordinateur.  
Le but de ces deux commandes est d'éviter la création de nouvaux Users/computers dans les OU par défaut d'ActiveDirectory.

*Le mappage de disque* présent dans les paramètres GPO permet de pouvoir mettre en commun un disque en évitant à la fois d'utiliser un script [Powershell](powershell.md) (quoique plus indiqué et peut-être plus simple) ou un script batch (qui ne permettra pas de confidentialité et est donc à proscrire).


# Détails complémentaires
## Sysvol (C:\Windows\SYSVOL par défaut)
Contient les scripts de connexions et le GPO.  
Pour le reste, voir : https://www.it-connect.fr/chapitres/le-partage-sysvol-et-la-replication/
## NTDS.DIT (C:\Windows\NTDS.DIT  par défaut)
