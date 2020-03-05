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

