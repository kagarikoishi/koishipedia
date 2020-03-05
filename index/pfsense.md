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

Rappel : Une DMZ est la séparation entre le "réseau de confiance" et le réseau Internet, qui n'a droit à aucune confiance.
Une DMZ doit aussi permettre de mettre des serveurs qui sont généralement à part du reste du réseau local et dont certaines informations peuvent passer à travers la DMZ (généralement par une translation d'adresse statique avec l'IP publique sur le port 80 et/ou 443 d'un coté et un port déteminé au ~hasard de l'autre.

   
     SRV-A   SRV-B   Pare-feu 
       |-------|-------[DMZ]----> Sortie
      DHCP               |
      PCs                |> Serveurs ex: - Apache
                                         - IIS

*Fig. 1 : Schéma d'architecture réseau que l'on voit en pratique*  

     SRV-A   SRV-B   Pare-feu                 Pare-feu de sorie du LAN
       |-------|-------[FW1]------------|----------------[FW2]----------[Routeur NAT/PAT*]---> Sortie WAN 1
      DHCP           TCP 1433           |          TCP 443 et 48653 (ex)            |            (VDSL)
      PCs                ||   Proxy <---|-->   Serveurs de gestion                  |
                      (qui filtre aussi le     et relations commerciale (CRM)       v
                       flux sortant)           Utilise le port SQL : TCP 1433     WAN 2 
                         ||                                 ||                    (4G)
          DMZ 2          ||             DMZ 1               || 
    =======================================================================================================
    *Idéalement un routeur capable de SD-WAN pour assurer une tolérance de panne.
  
*Fig.2 : Schéma d'architecture réseau qui devrait être idéalement appliqué*  

La DMZ peut aussi être entre deux pare-feux.  
Il faudrait -idéalement- aussi activer les antivirus/pare-feu et ne faire confiance à personne (concept zero-trust), car il est tout à fait possible d'infecter à partir d'un PC du réseau (voir à partir d'un sniffer...).  

De la même manière que la plupart des OS, il se configure à coup de Suivant/Suivant.
pfSesne à une tendance à refuser les modification post-configuration initiale, il faut donc penser son réseau avant d'installer l'UTM. Il s'administre via un serveur web, ce qui est très pratique (et donc installer Firefox sur les seveurs pour l'administrer...)   
Il a surtout un avantage : des plug-ins par milliards.
