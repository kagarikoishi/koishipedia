# Les bases d'Active Directory
____________________________   
Un article de Koishipédia   

Cet article est une partie à propos du fonctionnement de [Windows Server](windows-server-bases).   
  
  
Sommaire :   
	   
1. Présentation.
2. Les différents annuaires Active Directory
3. Le rôle DNS qui est enchâssé dans AD.
4. Les rôles FSMO
5. La gestion des groupes utilisateurs (GSG)
6. La gestion des politiques d'utilisation (GPO)

## Présentation
___________________
  
Active Directory est l'annuaire crée par Microsoft qui correspond au standard LDAP x500.  

L'Active Directory permet de créer un domaine, des groupes de sécurité (GSG) et ainsi de gérer un parc informatique de taille considérable.   
  
Il s'agit très certainement du dispositif Microsoft le plus fiable qui soit, ce qui est crucial du fait de son rôle.   
Active Directory a un certain nombre de composants que l'on retrouve dans sa version la plus répandue, l'AD-DS (Active Directory - Domain Controller), qui contient :
* Un serveur DNS (qui ne doit pas être installé préalablement à AD) et qui contient des pointeurs spécifiques à AD (SRV par exemple).  
* Un service Kerberos qui est une pseudo-infrastructure à clé publique (PKI) ayant pour but de sécuriser la communication.  
* Les rôles FSMO (dits *maîtres d'opérations*) qui sont là pour attribuer un maître à des rôles (Windows Server) qui en nécessitent (Active Directory étant capable de se répliquer et d'être piloté par n'importe lequel des contrôleurs de domaine AD).
* Des groupes d'utilisateurs ou groupe de sécurité, qui existent en quelque sorte dans les éditions client de Windows 10 (où ils ne peuvent pas être créés), tel que le groupe administrateur. AD permet de créer des groupes, qui sont souvent dans des Unités d'Organisation.
* Enfin nous avons les non moins importantes GPO, qui sont présentes dans toutes les versions de Windows (via gpedit.msc) et permettent de restreindre l'utilisateur de l'ordinateur.

## Les annuaires d'Active Directory
_________________
  
Active Directory existe en plusieurs déclinaisons, qui permettent d'avoir des rôles spécialisés :

***** Ebauche à combler *****

## Le rôle DNS d'Active Directory
____________________
  
Active Directory est fourni avec un DNS qui se sépare en deux parties : "mondomaine.local" et "\_msdcs" qui est endémique à AD et où s'installe le contenu nécessaire pour communiquer en tant que contrôleur de domaine.  Le DNS AD ne contient pas par défaut de zone de résolution inverse et est embarqué (comme presque tout le reste) dans C:\WINDOWS\NTDS.dit