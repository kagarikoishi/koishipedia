# Fonctionnement d'IPv4  
________

1. Pourquoi IPv4 ?   
2. Fonctionnement d'IPv4
3. Le bal masqué des adresses Internet  
4. Les classes (abrogées)  
5. Le protocole ARP  
____________

## Pourquoi IPv4 ?

Le protocole Internet version 4 est le premier protocole crée pour naviguer sur Internet, aux alentours de 1972. Simple d'utilisation par rapport à IPv6 (notamment du fait que son écriture soit en base décimale et assez courte pour être facilement retenue), elle a un certain nombre de contraintes qui lui sont propres : 
* C'est un vieux protocole qui a besoin d'autres protocoles qui sont d'une sécurité plus que relative (les attaques homme du milieu sont faciles).
* Il est problématique en WAN car la totalité des IP adressables (hors translation d'adresse / NAT) est limitée à 4,2 milliards d'adresses.
* Il n'est "pas fiable" ; une route décidée par IP peut fermer d'un seul coup ; les paquets vont alors disparaître et devront être réémis. 
* Il est cependant utilisé par toutes les interfaces d'administation matérielles (car il est pratiquement impossible de retenir une adresse IPv6).
* Il est connu et utilisé par tous les admins réseau.

## Fonctionnement d'IPv4

    Entête IP : 24 octets (b = bits, o = octet)
    ###########################################################################################
    ## Vers | IHL # Svc # LgT # Etq | PFra # TTL # Pro # CRC # IP. src # IP. dst #   Option  ##
    ##  4 b | 4 b # 1 o # 2 o # 3 b | 13 b # 1 o # 1 o # 2 o #   4 o   #   4 o   #  0 - 40 o ##
    ###########################################################################################
    Vers : version, IHL : Internet Header Length, Svc : Service, LgT : Longueur Totale, 
    Etq : étiquette (flag), PFra : Position Fragment, TTL : Time to Live, Pro : Protocole L4, 
    CRC : somme de contrôle,

IPv4 se greffe au-dessus [de la couche liaison](liaison.md) et en adopte des contraintes ; la couche liaison dicte la taille maximale des paquets (MTU), et a pour but et unique fonction de pouvoir transférer un paquet d'une source à une destination.  
Paradoxalemement c'est probablement le protocole Internet le plus connu (avec [IPv6](ipv6.md)), notamment du fait qu'il est indispensable au fonctionnement des protocoles applicatifs DNS que tout le monde utilise [(DNS permet de lier une adresse IP à un nom et un FQDN](dns.md)) et DHCP qui alloue automatiquement une IP a un poste donné.

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

## Le protocole ARP (EtherType 0x806)

ARP est une table qui a pour but d'associer une adresse MAC à une adresse IP.   
Pour ce faire, ARP envoie une demande en broadcast MAC en demandant "who is 192.168.1.1 ?". Le périphérique qui a l'adresse IP demandée répondra qu'il l'a. Tout comme [les tables MAC](liaison.md), les tables ARP sont horodatées.  
Un périphérique fait une demande ARP pour l'horodatage (2 mn sous Windows), mais aussi quand il doit communiquer avec une adresse IP qui est dans son réseau et non connue de sa table IP.
