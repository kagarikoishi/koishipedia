## Apprivoiser le dragon pfSense en quelques étapes  

Pfsense est un UTM (Unified Threat Management) qui fournit un ensemble de services ;
* du routage
* du VPN
* du DHCP
* et même un DNS
* un firewall
* de l'IDS et du IPS
* un portail captif...

Basé sur OpenBSD, il fait bien (mais sans plus face à des équipements dédiés), bien qu'il se démarque de ses concurrents par le fait qu'il soit un logiciel libre (contrairement à Kwartz...) et sa popularité (par opposition à Alcasar).
pfSense commercialise également du matériel dédié.

   
     SRV-A   SRV-B   Pare-feu 
       |-------|-------[DMZ]----> Sortie
      DHCP               |
      PCs                |> Serveurs ex: - Apache
                                         - IIS

*Fig. 1 : Schéma d'architecture réseau que l'on voit en pratique*
Rappel : Une DMZ est la séparation entre le "réseau de confiance" et le réseau Internet, qui n'a droit à aucune confiance.
Une DMZ doit aussi permettre de mettre des serveurs qui sont généralement à part du reste du réseau local et dont certaines informations peuvent passer à travers la DMZ (généralement par une translation d'adresse statique avec l'IP publique sur le port 80 et/ou 443 d'un coté et un port déteminé au ~hasard de l'autre.

     SRV-A   SRV-B   Pare-feu      Pare-feu avec NAT/PAT
       |-------|-------[DMZ]-----------------------------[DM2]---------------------> Sortie
      DHCP            TCP-1433          |           TCP-443 et 48653 (ex)
      PCs                               |> Serveurs de gestion
                                          et relations commerciale (CRM)
                                          Utilise le port SQL : le 1433
*Fig.2 : Schéma d'architecture réseau qui devrait être idéalement appliqué*
La DMZ peut aussi être entre deux pare-feu
