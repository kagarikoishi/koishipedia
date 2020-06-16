# IPv6
## Fonctionnement

Il arrive que le routage IPv6 ne soit pas activé par défaut sur les routeurs : dans le cas des routeurs cisco il faudra entrer au préalable la commande `ipv6 unicast-routing`

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

  * Voici la liste des options de l’entête IPv6 :

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

## Types d'adresses

Une adresse IPv6 se divise en :
* 64 bits pour le préfixe, dont :
  * 48 bits de routage global.
  * 16 bits pour un identifiant de sous-réseau.
* 64 bits pour l'identifiant de l'interface.

Il n'exite pas d'adresse broadcast pour IPv6, il est utilisé à la place une adresse de multidiffusion. Voici les préfixes qui permettent de définir le type d'adresse :

* unicast / monodiffusion :
  * 2001:: /16 : Adresse de monodiffusion globale ; routable, configurables automatiquement via SLAAC et DHCPv6.
  * FC00:: à FDFF:: / 7 : Adresses locales uniques
  * FE80:: à FEBF:: / 10 : Adresses link-local (équivalent à APIPA)
* multicast
  * ne peuvent être que des adresses de destination.
  * FFO2::1 : groupe de multidiffusion que tt le monde peut rejoindre.
  * FFO2::2 : groupe de multidiffusion que tt les routeurs peuvent rejoindre.
* anycast

### Adresses spéciales

* ::ffff:0:0 / 96 : Adresse IPv4 vers IPv6.
* ::1 / 128 : Bouclage local
* :: / 128 : route par défaut
* 2001:DB8:: / 32 : Exemple d'adresse pour les documentations.

## Protocoles spécifiques.

Sans état, 1re annonce
* SLAAC : permet de faire un équivalent de DHCP sans serveur spécifique, qui communique via ICMPv6. Le routeur fait passer un message d'annonce par défaut toutes les 200 secondes et aussi à tout hôte qui envoie une sollicitation de routeur via ICMPv6.

Stateless DHCPv6
* SLAAC pour créer l'adresse IP et DHCP pour le DNS et le nom de domaine.

* Statefull DHCPv6 = DHCP.

* Lorsque le message d'annonce de routeur est la SLAAC seule ou la SLAAC avec DHCPv6 sans état, le client doit générer lui-même son ID d'interface. Le client connaît la partie préfixe de l'adresse grâce au message d'annonce, mais il doit créer son ID d'interface. Pour cela, il peut utiliser la méthode EUI-64 ou un nombre à 64 bits généré aléatoirement, comme le montre la figure 1.

  * Un ID d'interface EUI-64 est représenté au format binaire et comprend trois parties :

  * le code OUI sur 24 bits, provenant de l'adresse MAC du client, mais dont le septième bit (universellement/localement, U/L) est inversé. Cela signifie que si le septième bit est un 0, il devient un 1, et vice versa.

  * La valeur de 16 bits FFFE intégrée (au format hexadécimal).

  * ID de périphérique de 24 bits de l'adresse MAC du client.

  * Le problème de confidentialité crée par cette méthode fait qu'il est préférable d'avoir une version avec un nombre aléatoire généré au lieu d'avoir son adresse MAC tatouée sur l'IP, et l'utilisation du protocole DAD pour vérifier l'unicité de son adresse.

* Une adresse de multidiffusion de nœud sollicité est comparable à une adresse de multidiffusion à tous les nœuds. Elle offre l'avantage d'être mappée à une adresse de multidiffusion Ethernet spéciale. Cela permet à la carte réseau Ethernet de filtrer la trame en examinant l'adresse MAC de destination sans l'envoyer au processus IPv6 pour voir si le périphérique est la cible prévue du paquet IPV6.

## Avantages et inconvéinents d'IPv6

* En-tête simplifiée
* Plus de données utiles et un meilleur transport
* Plus de protocole ARP et disparition de la faille béante qu'il représente.
* Configuration automatique des adresses (via DHCP6 ou SLAAC)
* NAT non-indispensable.
Mais aussi
* Fin des adresses privées
* Des adresses compliquées à retenir par rapport à l'ipv4
* Le calcul d'adresse plus difficile à faire de tête avec la base héxadécimale.
* Une transition longue et compliquée demandant l'utilisation de protocoles supplémentaires.

## Faire la transition entre IPv4 et IPv6

Il existe trois manières de le faire :

* Double pile : les périphériques utilisent les deux protocoles IP à la fois, ce qui ne nécessite pas de traduction.
* Par "tunneling" : les paquets v6 sont encapsulés dans des paquets v4.
* En traduisant : traduction des adresses réseau 64 (NAT64) qui traduit un paquet v4 en v6.
