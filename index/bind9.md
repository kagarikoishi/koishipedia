# Configuration du serveur DNS Bind9
c'est pas bien compliqué.

Pour modifier son DNS sur une machine Linux il faudra modifier le fichier /etc/resolv.conf et ajouter/modifier `nameserver 127.0.0.1`

Requêtes DNS : récursive ; le serveur DNS utilise un cache pour renvoyer le résultat d'une requête DNS.
Requête itérative : la requête DNS repart de là ou elle vient.

Schéma :   
requête itérative

    [PC]
      | recherche du site lol.com
      |
    [DNS local]  >>>>>>>> [Serveur racine]
      |          <<<<<<<< (réponse : .com est 2.4.6.8)
      |           
    [DNS local] >>>>>>>>>> [DNS TLD .com (2.4.6.8)]
      |         <<<<<<<<<< (réponse : lol.com est 2001:db8::ac46)
      v
    lol.com (page HTML)          

requête récursive (en général entre l'utilisateur et le redirecteur DNS, ex : 9.9.9.9)

    [PC]
      | recherche du site lol.com
      |
    [DNS local] (réponse : lol.com est 2001:db8::ac46)
      |          contenue dans le cache (à cause d'une précédente requête)
      |                        
      v
    lol.com (page HTML)          

A noter qu'un fichier peut être pointé par plusieurs DNS et avoir plusieurs noms (alias : on parlera de CNAME et DNAME) ; lol.com et w1.ptdr.local pointent par ex. sur la même page.

Les pointeurs :
IN : pointer vers Internet

A : vers une adresse IPv4  
NS : pointe un serveur de noms
AAAA : vers une adresse IPv6  
MX : Mail Exchange  
SRV : pointe vers un Service (modalité, TTL... d'un enregistrement)    
CNAME : alias d'un enregistement
DNAME : alias d'un répertoire NS

PTR : pointeur inverse

Glue record :
exemple.org NS ns1.exemple.org > Peut devenir une référence circulaire
exemple.org NS ns2.exemple.org
ns1.exemple.org A 192.168.29.1 > Pointeur A qui évite une référence circulaire
ns2.exemple.org A 192.168.30.1


LE DNAME permet de modifier un domaine entier, ainsi on peut déguiser publicite.fr en cestpourvotrebien.maru.com, que les liste des logiciels antipub ne conaissent pas ; ainsi non seulement cestpourvotrebien.maru.com mais aussi mail.cestpourvotrebien.maru.com pointeront respectivement vers publicite.fr et mail.publicite.fr

UN CNAME ne pointera jamais mail.pasdelapub vers publicite.fr.


    $TTL=86400 ;TTL=24h
    ;Zone maru.com
    @                     IN  CNAME       www
    ns1                   IN  A           172.16.1.1
    ns2                   IN  A           172.16.1.2
    www                   IN  A           172.16.1.10
    cestpourvotrebien     IN  DNAME       publicite.fr
    pasdelapub            IN  CNAME       publicite.fr

Et un DNS complet sous Bind (le fichier /etc/bind/db.dns.local)
