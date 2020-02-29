## Configuration de la sélection du pont racine et des ports racines, désignés et non-désignés 
    Switch(config)# spanning-tree vlan vlan-id root primary 
    Switch(config)# spanning-tree vlan vlan-id root secondary Switch(config)# spanning-tree vlan vlan-id priority value 
    Switch(config-if)# spanning-tree cost value 
    Switch(config-if)# spanning-tree port-priority value 
    Switch# show spanning-tree [detail | active] 
Les ports d’accès (qui ne sont pas reliés à des switch) peuvent être activé sans calculer de spanning tree (portfast). 
Mais dans ce cas, il faut sécuriser le cas où on branche un switch par erreur. 
Par exemple en coupant le port si on voit passer un paquet bpdu (qui servent au calcul de spanning tree) : 

## pour une interface 
    Switch(config-if)# spanning-tree portfast 
    Switch(config-if)# spanning-tree bpduguard # pour le faire par défaut sur tout les port d’accès 
    Switch(config)# spanning-tree portfast default 
    Switch(config)# spanning-tree portfast bpduguard
Le port est coupé, on peut le réactiver automatiquement après un certain temps 
    Switch(config)# errdisable recovery cause bpduguard 
    Switch(config)# errdisable recovery interval 400 
    
## Configuration de Rapid-PVST+ : 
    Switch(config)# spanning-tree mode rapid-pvst 
    Switch(config)# interface type port S
    witch(config-if)# spanning-tree link-type point-to-point 
    Switch(config-if)# end 
    Switch# clear spanning-tree detected-protocols
