# IPv6 
## Fonctionnement
### En-tête

    Longueur de l'en-tête sans options : 40 octets (320 bits).
    ###########################################################
    ## Ver # Cla # Label # Lng # Ets # TTL # IP src # IP dst ##
    ## 4 b # 1 o #  20b  # 2 o # 1 o # 1 o #  16 o  #  16 o  ##
    ###########################################################
   
    Label : étiquetage de flux.
    Cla : classe
    Lng : longueur
    Ets : entête suivante (next header)
    TTL : saut maximum (hop limit)
       

* Version : ce champ contient une valeur binaire de 4 bits définie sur 0110 indiquant qu'il s'agit d'un paquet IP version 6.

*  Classe de trafic : ce champ de 8 bits est l'équivalent du champ de services différenciés pour l'IPv4.

* Étiquetage de flux : ce champ de 20 bits indique que tous les paquets portant la même étiquette de flux doivent être traités de la même manière par les routeurs.

* Longueur des données utiles : ce champ de 16 bits indique la longueur de la partie données (utiles) du paquet IPv6. 
    
* Options d'en-tête suivante IPv6. Tout comme chez IPv4 le champ indique quel est le protocole suivant.
 
  * Voici la liste des protocoles les plus connus :

        01 – 00000001 – ICMP
        02 – 00000010 – IGMP
        06 – 00000110 – TCP
        17 – 00010001 – UDP
        58 – 00111010 – ICMPV6

  * Voici la liste des options de l’entête IPv6 vues plus bas :

        00 – Option Sauts après sauts
        60 – Option Destination
        43 – Option Routage
        44 – Option Fragmentation
        51 – Option AH
        50 – Option ESP

* Limite du nombre de tronçons : ce champ de 8 bits remplace le champ de durée de vie (TTL) de l'IPv4. Cette valeur est réduite d'un point chaque fois qu'un routeur transmet le paquet. Lorsque le compteur atteint 0, le paquet est rejeté et un message ICMPv6 de délai dépassé est transféré à l'hôte émetteur, indiquant que le paquet n'a pas atteint sa destination en raison du dépassement du nombre limite de tronçons.

* Adresse source IPv6 : ce champ de 128 bits identifie l'adresse IPv6 de l'hôte émetteur.

* Adresse IPv6 de destination : ce champ de 128 bits identifie l'adresse IPv6 de l'hôte destinataire.

Un paquet IPv6 peut également contenir des en-têtes d'extension qui fournissent des informations facultatives de couche réseau. Les en-têtes d'extension sont facultatifs et sont placés entre l'en-tête IPv6 et les données utiles. Ils sont utilisés pour la fragmentation, la sécurité, la prise en charge de la mobilité, etc.

Contrairement à IPv4, les routeurs ne fragmentent pas les paquets IPv6 routés.

## Avantages et inconvéinents d'IPv6 

* En-tête simplifiée
* Plus de données utiles et un meilleur transport (et pas d'ARP)
* Configuration automatique des adresses (pas besoin de dhcp?)
* NAT non-indispensable.

    
