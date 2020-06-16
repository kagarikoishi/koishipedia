# Activer le routage sur un PC ordinaire (port forwarding).
Il existe seulement deux méthodes pour ce faire.  

* Sous Windows il faut changer la clé de registre  
` HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters`
et mettre la valeur `IPEnableRouter` à 1.

* Sous Unix il faudra activer le port forwarding :
  1. éditer le fichier sysctl.conf et y décommenter   
  `net.ipv4.ip_forward=1`
  `net.ipv6.conf.all.forwarding=1`
  2. Vérifier le fonctionnement : `sudo sysctl -p`
  3. Ajouter la règle suivante sur IPtables, eth0 pointant vers Internet :
  `sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE`
  4. Sauvegarder la règle demande d'installer iptables-persistent.
  Si il est installé, il faudra faire `sudo dpkg-reconfigure iptables-persistent`. ou :  
  `iptables-save > /etc/iptables/rules.v4`  
  `ip6tables-save > /etc/iptables/rules.v6`
