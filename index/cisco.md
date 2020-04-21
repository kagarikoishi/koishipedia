# Commandes de base de Cisco iOS
 Un article de Koishipédia   
   
	   
 
## Liste des commandes de base
_____________________  

#### Cette liste de commande liste les commandes essentielles du mode "console" de Cisco iOS.   
La plupart de ces commandes seraient communes au mode console d'autres systèmes.   

#### La hiérarchie d'exécution (l'ordre à respecter) est comme suit :
   
> Commande de lancement du terminal  
>   
> Commande de vérification (show \*),  
> > Commande de configuration,  
> > > Paramétrages d'interface .  
   
<br>
	 
### Liste des commandes
_____________
	
> enable : lance le terminal. 
> **sh**ow ip [route] [address] [nat translations] : Montrer les routes/adresses/... configurées sur le routeur.  
> 
> ping, tracert : identique aux OS client/serveur 
>  
> debug ip rip : vérifie la table de routage du protocole RIP  
>   
> **ex**it : sortir d'un niveau de terminal   
> 
> > **conf**igure **t**erminal : Entre en mode privilégié (configuration)  
> >   
> > ip route 0.0.0.0 "réseau distant" 0.0.0.0 "sous-masque IP" 0.0.0.0 "passerelle" : Définir une route  
> >   
> >  **in**terface  "type :" **gi**gabitethernet 0/0 "numéro" : Configurer une interface réseau (FastEthernet, GigabitEthernet, Ethernet)
> >  > **ip addr**ess  172.22.10.20 "adresse ip" 172.22.10.128 "passerelle" : définir l'adresse IP de l'interface.  
> >  >   
> >  > **no sh**utdown : Mise en service de l'interface (hors-service par défaut sur un routeur)   
> >  > 
> >  > **sh**utdown : Fermeture de la connexion.  
> >  >   
> >  > **ip nat in**side : définit l'interface comme le coté interne du NAT/PAT.  
> >  >    
> >  > **ip nat ou**tside : définit l'interface comme le coté externe du NAT/PAT.   
>>
> >  **ro**uter **rip** : Entrer sur l'interface de routage RIP.  
> >  >  
> >  >  **v**ersion **2** : par défaut la V1 est utilisée (qui utilise le [mécanisme des classes](ipv4.md))  
> >  >    
> >  >  **no au**to-summary : Empêche l'agrégation des routes (et utiliser des adresses classless)  
> >  >    
> > >  **ne**twork [87.211.103.224]("ip réseau")  : Ajouter un réseau à la table RIP
>
> **Première méthode pour créer un NAT/PAT automatique**   
>
>>  access-list [1] permit "ip privée" "Masque inverse" : Créer une liste d'accès de translation vers le NAT
>>   
>>  ip nat inside source list [1] int [fa 0/1] overload :  C'est une redirection d'adresse (NAT-PAT). int fa 0/1 est l'interface outside.  
>
>**Deuxième méthode pour créer un NAT/PAT automatique**   
>
>>   ip nat pool sortie "première IP de sortie" "dernière IP de sortie" netmask "masque" : étend une plage d'IP qui sert à faire la translation de masque.  
>>   
>> ip nat source list [1] sortie : active le NAT.   
>> 
>> ip nat inside source static TCP "IP interne" "Port TCP" "IP externe" "Port TCP" : crée une redirection NAT/PAT sur un port spécifique (bien souvent au niveau du port 80 et 443 (HTTP et HTTPS) pour ne pas pointer vers l'adresse IP privée du serveur.  
>  
> **copy run st**art : Pour sauvegarder la configuration en cours (running-config) en tant que celle de démarrage du routeur/switch.  

# Créer un spanning-tree.
---------
### Configuration de la sélection du pont racine et des ports racines, désignés et non-désignés 
    Switch(config)# spanning-tree vlan vlan-id root primary 
    Switch(config)# spanning-tree vlan vlan-id root secondary 
    Switch(config)# spanning-tree vlan vlan-id priority value 
    Switch(config-if)# spanning-tree cost value 
    Switch(config-if)# spanning-tree port-priority value 
    Switch# show spanning-tree [detail | active] 
Les ports d’accès (qui ne sont pas reliés à des switch) peuvent être activé sans calculer de spanning tree (portfast). 
Mais dans ce cas, il faut sécuriser le cas où on branche un switch par erreur. 
Par exemple en coupant le port si on voit passer un paquet bpdu (qui servent au calcul de spanning tree) : 

### pour une interface 
    Switch(config-if)# spanning-tree portfast 
    Switch(config-if)# spanning-tree bpduguard # pour le faire par défaut sur tout les port d’accès 
    Switch(config)# spanning-tree portfast default 
    Switch(config)# spanning-tree portfast bpduguard
Le port est coupé, on peut le réactiver automatiquement après un certain temps 
    Switch(config)# errdisable recovery cause bpduguard 
    Switch(config)# errdisable recovery interval 400 
    
### Configuration de Rapid-PVST+ : 
    Switch(config)# spanning-tree mode rapid-pvst 
    Switch(config)# interface type port S
    Switch(config-if)# spanning-tree link-type point-to-point 
    Switch(config-if)# end 
    Switch# clear spanning-tree detected-protocols

# Raccourcis de Cisco IOS (non courants):
* `Ctrl+K` Efface tous les caractères à partir du curseur.
* `Ctrl+U ou Ctrl+X` Efface tous les caractères jusqu'au curseur.
* `Esc+D` Efface le prochain mot à partir du curseur.
* `Ctrl+W` Efface le mot précédant le curseur.
* `Esc+B, Esc+F` Déplace le curseur d'un mot à gauche ou à droite.
* `Ctrl+Maj+6` Interrompt les recherches DNS, ping et traceroute.
* `Ctrl+R/I/L` Rappelle une ligne interrompue par un message IOS (du genre `GigabitEthernet0/0 is up`).
* `Espace` dans le cas d'une commande `| more`, permet de changer d'écran.

