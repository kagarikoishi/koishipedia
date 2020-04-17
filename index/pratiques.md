# Les bonnes pratiques.
### Pratiques de base en sécurité.
* Ne jamais utiliser un compte administrateur nommé admin
* Ne jamais utiliser un mot de passe évident ou stupide
* Bannir autant que possible les mots de passe et les remplacer par d'autres techniques (cartes à puce, gestionnaire de mots de passe...) Si c'est impossible, contraindre un mot de passe long.
* Ne jamais avoir de compte admin global utilisé de manière active (chaque sysadmin doit avoir son compte admin)
* Interdire le branchement de clés USB sur un ordinateur si ce n'est pas nécessaire.
* Monitorer son réseau.
* Avoir plusieurs backups prêtes à prendre le relais (qui doivent être stockées dans plusieurs endroits différents.
* Avoir plusieurs types de connexion à son entreprise (qui doivent être de type différent ; prendre deux abonnements fibre optique qui passent par un même point n'a aucun intérêt, il faut que :
	* Celles-ci soient opérées par deux opérateurs distincts (évitant la chute du réseau dans le cas ou un serveur principal d'un opérateur tombe)
	* Celles-ci soient désormais opérées en SD-WAN, afin de pouvoir faire des reports de charge instantanés, notamment pour ce qui ne supporte pas la latence (ex : la téléphonie qui est prioritaire sur le reste) ou éviter une coupure de connexion qui peut être fatale au niveau d'un document.
* Ne jamais utiliser VLAN 1, 10, 20 et 99 par défaut ou comme VLAN principaux ; leur utilisation est si répandue qu'un bon pirate peut aisément les attaquer.
* Ne jamais laisser un switch administable sans spanning tree, et aussi :
	* Eviter que l'interface d'administation du switch soit sur son adresse par défaut - lui donner une autre adresse
	* Limiter les ports d'administration autant que possible, sinon s'assurer de l'impossibilité de modifier les branchements du switch sans autorisation, en laissant celui-ci dans un local ou une armoire fermée à clé (qui est rangée dans un local approprié ; le coffre-fort de la salle des serveurs qui contient les autres clés en plusieurs exemplaires et celles des baies de brassage)
* Ne jamais demander le mot de passe d'autrui,  quitte à devoir exploiter les failles de l'ordinateur pour créer un nouvel utilisateur administrateur. Prendre la place d'autrui signifie aussi risquer de prendre sa responsabilité pour **ses** actes.  
* Ne pas réparer les ordinateurs personnels de ses employés sans un contrat. Ils peuvent se retourner contre vous.
* Si $USER a été viré(e), effacer son compte d'Active Directory ou au moins ses autorisations (dans le cas où ce compte ne peut être effacé ou l'employé est susceptible d'être rembauché).

### Pratiques à faire.
* Sourire et être aimable. Faire comme si les employés étaient des enfants peut aider (mais ça a ses limites).
* Cabler proprement et documenter ses schémas réseau. 
* Etiqueter proprement toutes les baies de brassage.
* Documenter ce que l'on fait dans la mesure où il est possible d'oublier ce que l'on a fait. Dans le cas où l'on risque de se faire virer car il suffit de lire la doc, prétendre qu'elle n'a pas été faite (que vous le faites de tête) ou est perdue. 
* Aider les utilisateurs à utiliser leur matériel mais prendre son temps avant d'arriver -- temporiser dix minutes avant de répondre afin d'éliminer les utilisateurs qui n'ont pas envie de faire eux-même quelque chose qu'ils savent faire.
* Leur faire faire les manipulations qu'ils devraient savoir faire. Il faudra souvent le répéter plusieurs fois.
* Quand il est l'heure des explications et des comptes rendus, le faire de manière simple ; éviter une explication trop longue (l'auditoire s'endormira), trop expéditive (l'auditoire n'a pas le temps de comprendre) ou trop compliquée (pas mieux). Ecrire ses conseils pour des débutants est une bonne chose, sauf si l'auditoire à un bon niveau dans le domaine et peut comprendre directement les concepts abordés.  Faire des pauses de quelques minutes au moins une fois par heure.
* Imager ce que l'on va dire ; faire des allusions à des choses simples et claires pour transposer un concept compliqué.
	* par exemple ; un serveur mandataire (ou proxy) est un entremetteur entre vous et la personne à qui vous n'osez pas parler.

Koishipédia, version n°1 du 25 Février 2020 / 20:26

# D'autres bonnes pratiques
## Gérer un projet.
Il faut agir de manière simple et logique : de petites tâches, une forte automatisation des procédures (une procédure pour tout ce qui risque d'arriver, en commençant par celles qui seront reproduites 14000 fois (changer un mot de passe...), en appliquant un système de gestion par type (incident, panne, problèmes, application de projets, test, production).
Si cela a une certaine lourdeur (puisque cela implique beaucoup d'applicatif -idéalement automatisée, au moins au niveau de la description du fait/incident puisqu'il est peu probable qu'un commercial sache ce qu'est une erreur de segmentation...  
Néanmoins cela signifie que la personne en charge de la gestion du SI (le fameux DSI) doit être au fait de l'art de la gestion de projet (**références ITIL par ex**), ne doit pas avoir une forte délégation (qui provoque une lourdeur extrême et empêche une réaction rapide puisqu'il faudra 33120 réunions pour adopter une solution).

Mais avant de lancer un projet, il est sain et logique de se demander, indépendament de la méthode :

#### Lancer un projet.
* Le projet est-il utile et réalisable ?
* Le projet est-il pertinent (il peut être utile sans qu'il y ait un intérêt à le réaliser).
* Le projet est il prioritaire ? (éviter de faire un projet qui se base sur quelque chose qui n'existe pas encore).
* Quelles ressources sont allouables au projet (prix et moyens humains, temps a réaliser)
#### Continuer un projet
* Le projet est-il encore pertinent **(à ne surtout pas mettre en parallèle aux avancées déja faites et aux moyens mis en place)**
	* Autrement dit, le projet est-il devenu un coût irrécupérable ?
		* Le contenu du projet est-il réutilisable ?
		* Ou faut-il juste arrêter le projet car il est inutilisable en l'état ?
* Le projet est-il encore prioritaire ou non.
	* Continuer sur le projet
	* Allouer plus de moyens si il est prioritaire.
	* Mettre en pause le projet si non prioritaire.
* Le projet est-il en train de devenir trop complexe ?
	* Faut-il le diviser en nouvaux sous-projets ?
	* Faut-il allouer plus de moyens (en personnel) et / ou de responsabilités ?
	* Faut-il déléguer le projet à des personnes plus compétentes ?
* Faut-il repenser la gestion du projet ?
#### Achèvement du projet
* Est-il temps de condsidérer le projet comme achevé et passer à autre chose ?
* Il est temps de le tester avant de l'envoyer en production.

	
