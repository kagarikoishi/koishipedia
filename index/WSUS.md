## Gérer les mises à jour : 

Elles ont lieu tous les 2e mardi du mois à 18h.

* Par niveau de criticité
* Par site
* Par type de faille
	* Faille zero day (découverte de la faille par le monde de la sécurité
	* CVE ([vulnérabilité communes - un annuaire consultable](https://cve.mitre.org/))

* En fonction des failles
	* Exécution de code à distance	
	* Elevation de privilèges
	* Contournement de sécurité
	* Divulgation d'informations
	* Déni de service
	
* Classification des MAJ par date :
	* Obsolète - l'objet sous la faille est obsolète et donc la correction inutile
	* Superseeded - L'objet a subi une correction plus récente qui écrase la première.

Il faut maintenir un parc à jour, de manière progressive (lab/test puis échantillon de prod et enfin prod globale).
Ne pas oublier de tester longuement (tester les interrogations de BDD, des compatibilités brisées...).
Malgré le fait que chaque OS aura des failles non réglées, il faut se souvenir que l'on a des murailles qui protègent correctement et ne pas push trop tôt des MàJ (un mois de décalage est acceptable). Certaines entreprises les font passer dès que possible (ex. BNP Paribas).

## Configurer WSUS.



