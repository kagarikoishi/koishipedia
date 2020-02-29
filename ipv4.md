# Fonctionnement d'IPv4  
________

1. Pourquoi IPv4 ?   
2. Le bal masqué des adresses Internet  
3. Les classes (abrogées)  
4. Le protocole ARP  
____________

## Pourquoi IPv4 ?

Le protocole Internet version 4 est le premier protocole crée pour naviguer sur Internet, aux alentours de 1972. Simple d'utilisation par rapport à IPv6 (notamment du fait que son écriture soit en base décimale et assez courte pour être facilement retenue), elle a un certain nombre de contraintes qui lui sont propres : 
* C'est un vieux protocole qui a besoin d'autres protocoles qui sont d'une sécurité plus que relative (les attaques homme du milieu sont faciles).
* Il est problématique en WAN car la totalité des IP adressables (hors translation d'adresse / NAT) est limitée à 4,2 milliards d'adresses.
* Il est cependant utilisé par toutes les interfaces d'administation matérielles.
* Il est connu et utilisé par tous les admins réseau.

## Les classes IP

Les classes en IPv4 est un concept abrogé depuis longtemps mais encore utilisé par les logiciels pour essayer de calculer automatiquement les masques de sous-réseau. Il existe quatre classes.   

* **0**0000000 00000000 00000000 00000000 / 8 : Ceci est la classe A. Le premier bit définit la plage ; 0.0.0.0 à 127.0.0.0
*  **10**000000 00000000 00000000 00000000 / 16 : Classe B. Plage de 128 à 192.
*   **110**00000 00000000 00000000 00000000 / 24 :  Classe C. Plage de 192 à 223.
*    **1110**0000 00000000 00000000 00000000 / 30 :  Classe D. Plage de 224 à 240 (expérimental).

Les IP non routables sont assimilées aux classes, mais de fait celles-ci sont hors-classe. Les RFC les définissent ainsi :   
 
*  10.0.0.0 / 8           -   10.0.0.1 à 10.255.255.254
*  172.16.0.0 / 12    -   172.16.0.1 à 172.31.255.254
*  192.168.0.0 / 16  -   192.168.0.1 à 192.168.255.255

S'y ajoutent aussi les adresses non-attribuables : 

* 127.0.0.1
* 0.0.0.0 qui permet d'envoyer vers n'importe qui (fréquent en attribution statique d'une route IP)
* 255.255.255.255 qui est une adresse du sous-masque et par définition inattribuable. 
