# Fonctionnement d'IPv4  
________

1. Pourquoi IPv4 ?   
2. Fonctionnement d'IPv4
3. Le bal masqué des adresses Internet  
4. Les classes (abrogées)  
5. Les adresses de multidiffusion
6. Le protocole ARP  
____________

## Pourquoi IPv4 ?

Le protocole Internet version 4 est le premier protocole crée pour naviguer sur Internet, aux alentours de 1972. Simple d'utilisation par rapport à IPv6 (notamment du fait que son écriture soit en base décimale et assez courte pour être facilement retenue), elle a un certain nombre de contraintes qui lui sont propres :
* C'est un vieux protocole qui a besoin d'autres protocoles qui sont d'une sécurité plus que relative (les attaques homme du milieu sont faciles).
* Il est problématique en WAN car la totalité des IP adressables (hors translation d'adresse / NAT) est limitée à 4,2 milliards d'adresses.
* Il n'est "pas fiable" ; une route décidée par IP peut fermer d'un seul coup ; les paquets vont alors disparaître et devront être réémis.
* Il est cependant utilisé par toutes les interfaces d'administation matérielles (car il est pratiquement impossible de retenir une adresse IPv6).
* Il est connu et utilisé par tous les admins réseau.

## Fonctionnement d'IPv4

### En-tête et description.

    Entête IP : 24 octets (b = bits, o = octet)
    #############################################################################################
    ## Vers | IHL # Svc # LgT # Id. # Etq | PFra # TTL # Pro # CRC # IP. src # IP. dst #  Opt  ##
    ##  4 b | 4 b # 1 o # 2 o # 2 o # 3 b | 13 b # 1 o # 1 o # 2 o #   4 o   #   4 o   #  40 o ##
    #############################################################################################
    Vers : version, IHL : Internet Header Length, Svc : Service, LgT : Longueur Totale,
    Id. Identification, Etq : étiquette (flag), PFra : Position Fragment, TTL : Time to Live,
    Pro : Protocole L4, CRC : somme de contrôle,

* Version : ce champ contient une valeur binaire de 4 bits définie sur 0100 indiquant qu'il s'agit d'un paquet IP version 4.

* Services différenciés ou DiffServ (DS) : anciennement appelé champ de type de service, le champ Services différenciés est un champ de 8 bits utilisé pour définir la priorité de chaque paquet. Les six bits de poids fort du champ DiffServ sont représentés par le marquage DSCP (Differentiated Services Code Point) et les deux derniers bits sont des bits ECN (Explicit Congestion Notification).

* les champs Identification, Indicateurs et Décalage du fragment pour garder la trace des fragments. Un routeur peut être amené à fragmenter un paquet pour le transmettre d'un support à un autre, dont la MTU est inférieure.

* Time-to-live (durée de vie, TTL) : ce champ contient une valeur binaire de 8 bits utilisée pour limiter la durée de vie d'un paquet. L'expéditeur du paquet définit la valeur TTL initiale et celle-ci diminue d'un point chaque fois que le paquet est traité par un routeur. Si la valeur du champ TTL arrive à zéro, le routeur rejette le paquet et envoie un message de dépassement du délai ICMP (Internet Control Message Protocol) à l'adresse IP source.

* Le champ Protocole est utilisé pour identifier le prochain protocole de niveau. Cette valeur binaire de 8 bits indique le type de données utiles transportées par le paquet, ce qui permet à la couche réseau de transmettre les données au protocole de couche supérieure approprié. Les valeurs les plus courantes sont notamment ICMP (1), TCP (6) et UDP (17).

* Adresse IPv4 source : ce champ contient une valeur binaire de 32 bits, qui représente l'adresse IP source du paquet. L'adresse IPv4 source est toujours une adresse de monodiffusion.

* Adresse IPv4 de destination : ce champ contient une valeur binaire de 32 bits qui représente l'adresse IP de destination du paquet. L'adresse IPv4 de destination est une adresse de monodiffusion, de diffusion ou de multidiffusion.

### Description

IPv4 se greffe au-dessus [de la couche liaison](liaison.md) et en adopte des contraintes ; la couche liaison dicte la taille maximale des paquets (MTU), et a pour but et unique fonction de pouvoir transférer un paquet d'une source à une destination.  
Paradoxalemement c'est probablement le protocole Internet le plus connu (avec [IPv6](ipv6.md)), notamment du fait qu'il est indispensable au fonctionnement des protocoles applicatifs DNS que tout le monde utilise [(DNS permet de lier une adresse IP à un nom et un FQDN](dns.md)) et DHCP qui alloue automatiquement une IP a un poste donné.  

IP n'est pas connecté ; il ne pré-établit pas une route pour créer une liaison (ce que fait la commutation par définition), et donc va envoyer des paquets même si l'IP de destination est inaccessible (c'est la couche transport qui le fera, via des protocoles comme TCP), ne garantit pas l'arrivée de paquets et ajustera la taille du paquet en fonction du type de liaison.

## Les classes IP

Les classes en IPv4 est un concept abrogé depuis longtemps mais encore utilisé par les logiciels pour essayer de calculer automatiquement les masques de sous-réseau. Il existe quatre classes.   

 *  <strong>0</strong>0000000 00000000 00000000 00000000 / 8 : Ceci est la classe A. Le premier bit définit la plage ; 0.0.0.0 à 127.0.0.0
 *  <strong>10</strong>000000 00000000 00000000 00000000 / 16 : Classe B. Plage de 128 à 192.
 *  <strong>110</strong>00000 00000000 00000000 00000000 / 24 :  Classe C. Plage de 192 à 223.
 *  <strong>1110</strong>0000 00000000 00000000 00000000 / 30 :  Classe D. Plage de 224 à 240 (multidiffusion).

## IP spéciales

### IP non routables.

Les IP non routables sont assimilées aux classes, mais de fait celles-ci sont hors-classe. La RFC 1918 les définissent ainsi :   

*  10.0.0.0 / 8      -   10.0.0.1 à 10.255.255.254
*  172.16.0.0 / 12   -   172.16.0.1 à 172.31.255.254
*  192.168.0.0 / 16  -   192.168.0.1 à 192.168.255.255

### S'y ajoutent aussi les adresses non-attribuables :

* 127.0.0.1
* 0.0.0.0 qui permet d'envoyer vers n'importe qui (fréquent en attribution statique d'une route IP)
* 255.255.255.255 qui est une adresse de diffusion.

### Les adresses spéciales

Les blocs suivant sont utilisés de manière spécifique :

* 169.254.0.0 / 16 qui est utilisé par un client DHCP si il n'y a aucun serveur DHCP (APIPA).
* 192.0.2.0 / 24 sont des adresses d'essais pour de la documentation et ne sont pas routables (TEST-NET).
* 192.88.99.0 / 24 est réservée au relais anicast 6to4, voir RFC 3068.
* 198.18.0.0 / 15 est utilisé pour les tests de performances : RFC 2544.
* 240.0.0.0 / 4 qui est réservé pour une utilisation future : RFC 3330.

### La Multidiffusion

Les adresses de ce qui était la classe D (224.0.0.0 - 240.0.0.0) sont désormais des adresses de multidiffusion sur le réseau local.  
Celles-ci s'appliquent principalement aux protocoles de routage :

* Tous les périphériques du (sous) réseau : 224.0.0.1
* Tous les routeurs : 224.0.0.2
* OSPF utilise 224.0.0.5 (tous les routeurs) et 224.0.0.6 (Routeurs désignés)
* RIP v2 utilise 224.0.0.9
* EIGRP utilise 224.0.0.10
* DHCP utilise 224.0.0.12
* Teredo utilise 224.0.0.253


## Le protocole ARP (EtherType 0x806)

ARP est une table qui a pour but d'associer une adresse MAC à une adresse IP.   
Pour ce faire, ARP envoie une demande en broadcast MAC en demandant "who is 192.168.1.1 ?". Le périphérique qui a l'adresse IP demandée répondra qu'il l'a. Tout comme [les tables MAC](liaison.md), les tables ARP sont horodatées.  
Un périphérique fait une demande ARP pour l'horodatage (2 mn sous Windows), mais aussi quand il doit communiquer avec une adresse IP qui est dans son réseau et non connue de sa table IP.
