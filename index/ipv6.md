# IPv6 
## Fonctionnement
### En-tête

    ###########################################################
    ## Ver # Cla # Label # Lng # Ets # TTL # IP src # IP dst ##
    ## 4 b # 1 o #  20b  # 2 o # 1 o # 1 o #  16 o  #  16 o  ##
    ###########################################################
   
    Cla : classe
    Lng : longueur
    Ets : entête suivante (next header)*
    TTL : saut maximum (Hop Limit)
       
 * Options d'en-tête suivante IPv6. Tout comme chez IPv4 le champ indique quel est le protocole suivant.
 
  * Voici la liste des protocoles les plus connu :

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

    
