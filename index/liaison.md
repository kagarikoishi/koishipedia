# Les protocoles de liaison

## 1.1 : le visage d'une trame de liaison - MAC ([Wikipédia](https://en.wikipedia.org/wiki/Ethernet_frame))
    
    Longeur d'une trame Ethernet II : 64 à 1530 octets.
    -----------------------------------------------------------------------------
    | Préambule |SFD | MAC dst | Mac src |802.1Q| EtherType |   Données   | FCS |
    |    7 o    | 1o |   6 o   |   6 o   |  4o  |    2 o    | 46 à 1500 o | 4 o |
    -----------------------------------------------------------------------------
    
* SFD (1 octet) est utilisé à des fins de synchronisation.
* Préambule : permet au récepteur de se préparer à recevoir une nouvelle trame.
* MAC (Media Access Control) Destination : Adresse physique de destination
  * L'adresse MAC est séparée en plusieurs sous-champs : 
    * 1er bit : si 0 = unicast, 1 = multicast/broadcast (bit d'individualité)
    * 2e bit : si 0 = MAC définie par le constructeur (BIA), 1 = MAC définie par l'administrateur réseau
    * 3-24 (22) bits : Organization Unit Identifier (OUI, id. constructeur).
    * 25-48 (24) bits : **Valeur unique** de l'adresse MAC.
    L'adresse MAC est dite rémanente car l'adresse est codée dans la mémoire morte de la carte. Cependant il est possible (et facile) de la changer car elle est chargée dans la mémoire vive pour pouvoir être utilisée.
* MAC source : Adresse de la source. 
    * Certaines sources sont spéciales :   
    01-00-5E = Multidiffusion IPv4
    33-33 = Multidiffusion IPv6
    FF-FF-FF-FF-FF-FF = Diffusion (utilisées par DHCP et ARP).
    Les adresses de multidiffusion prennent le dernier octer de l'adresse IP du diffuseur.
* EtherType : Permet d'identifier le protocole encapsulé dans la trame Ethernet :   
  * 0x800  = IPv4
  * 0x86DD = IPv6
  * 0x806  = ARP
* 802.1Q : étiquette VLAN.
* Données : Des paquets. Doit faire au moins 64 bits (si inférieur MAC ajoutera un bourrage de zéro ou padding pour faire la taille correcte.
* FCS : Contrôle de redondance cyclique (CRC) pour l'intégrité de la trame. la CRC est calculée sur le nombre de bits à 1 de la trame.

Une trame Ethernet II est automatiquement rejetée si elle est plus courte que 64 octets ou plus longue que 1530 octets ou si le CRC est incohérent avec le message.

Le MAC (802.3) permet de prendre en charge les méthode CSMA/CD et CA (Collision Detection et Collison Avoidance pour la wifi), en convertissant les bits en trame.

## Logical Link Control

LLC (802.2) les transfère vers IP et ARP et sert d'intermédiare en tant que contrôleuse de la carte réseau.

## Les commutateurs (non-L3)
Ceux-ci traitent les protocoles de niveau 1 et 2 et sont donc constituées d'une table MAC (parfois dite CAM) et non des tables ARP. La table conserve par défaut l'adresse dans sa table 5 minutes.
Si l'adresse MAC est inconnue à la table MAC du commutateur, il la transfère à tout le monde sauf le port source.

### Commutation Store and Forward
Ce commutateur reçoit l'intégralité de la trame et calcule le CRC puis l'envoie a bon port si la trame est valide
### Commutation Cut-through
Celui-ci ne lit pas la totalité de la trame et s'arrête après avoir lu le destinataire.
 * Commutation fast-forward : envoie la trame dès que la destination de celui-ci est connue.
 * Commutation fragment-free : lit les 64 premiers octets de la trame et vérifie l'intégrité de cette partie. C'est un compromis entre le rapide FF et le lent Store et Forward. 
 Certains commutateurs sont en Cut-Through par défaut et passent en S et F si le seuil d'erreur est supérieur à un seuil défini.
 
 ### Tampons 
 Soit sur : 
 * La mémoire tampon est organisée en fonction des ports entrants et sortants. Les trames sont envoyées une par une. Une trame peut retarder la transmission des autres si son port de destination est saturé, même si les autres trames ne vont pas en destination du port saturé.
 * La mémoire tampon est partagée pour tous les ports. La mémoire est allouée dynamiquement aux ports de destination, et les trames sont liées de manière dynamique, ce qui évite d'avoir une file d'attente entre port entrant et sorant. Le commutateur tient alors une liste, peut supporter de plus grandes trames au détriment de plus petites si la mémoire et saturée.
 
Les commutateurs à mémoire tampon sont préférables pour des communications entres des pots à débits différents (avec x ports en 100 M/s et un en 1 Gb/s).
 
 La plupart des cartes réseau/sw. proposent la négociation automatique et choisissent le protocole le plus performant en fonction du périphérique le plus faible du lien.
 
 Le semi-duplex est un mode où un lien est duplex, mais chacun son tour. Si des ports est en semi-duplex et l'autre pas, cela provoquera de nombreuses collisions.
 
### Auto-MDIX
Détecte le type de cable connecté qu commutateur. Certaines interfaces réseau n'en sont pas équipées à partir de Cisco IOS 12 entre autres.

### ARP : voir la page [IPv4](IPv4.md)

