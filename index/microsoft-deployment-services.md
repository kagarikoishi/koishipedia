## Comment créer un déploiement Microsoft avec ses outils gratuits : MDT et ADK.
Etapes : 
* Installer les ADK ordinaires.
* Ensuite installer l'add-on Windows PE (ADK-PE).
* Et enfin installer Microsoft Deployment Toolkit.
* Ainsi que Serva ou WDS pour pouvoir déployer avec un PXE.
  
Une fois ces applications installées, il faudra alors aussi : 

* Une ISO (tout au moins l'image install.wim) de l'OS windows désiré.
* Une ou des applications qui auront pour but d'être préinstallées (ex : 7zip, firefox...), voire juste laisser des applications à faire déployer par l'utilisateur.

* Il est possible de créer des conditions pour installer les drivers selon les données constructeurs du PC (évitant la multiplication de masters au prix d'un poids plus lourd).

## Comment déployer concrètement ?

Pour déployer une machine, il va falloir d'abord rentre sur le Deployment Workbench, qui est la console enfichable qui permet de presque tout faire sur le déploiment.  
Il faudra

-----WIP------
