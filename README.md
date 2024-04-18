# CrowdSec-Easy-Installation 

''' Pour les personnes souhaitant tester entre deux VM, n'oubliez pas de mettre vos VM en BRIDGE et de lire la 4 ème étape '''

I/ Rendez-vous sur le site CrowdSec et cliquer sur le linux

II/ Installer les référentiels 
 - Ceci permettra d'accéder aux derniers packages de Crowdsec et ses composants de correction.
   -  Lancer la commande :

# sudo apt update
# sudo apt install curl
# sudo curl -s https://packagecloud.io/install/repositories/crowdsec/crowdsec/script.deb.sh | sudo bash


III/ Installer le moteur Crowdsec
 - L'outil Crowdsec sans son Bouncer permet d'alerter si quelqu'un tente d'exploiter une faille de sécurité,
   cependant il faudra avoir au préalable installer les collections/scénarios pour les logiciels en question.
   
 - Entrer cette commande pour installer l'outil :
   
   # sudo apt install crowdsec


III/ Installer un Bouncer 
 - Le bouncer permet de bloquer les tentatives de connexions
    - Entrer la commande pour installer le bouncer classique pour bloqué les IP

   # sudo apt install crowdsec-firewall-bouncer-iptables

IV/ Configurer les détections d'alertes 
 - Rendez-vous dans le dossier :
   
   # cd /etc/crowdsec/parsers/s02-enrich

 -  Puis éditer le fichier whitelists.yaml

   # sudo nano whitelists.yaml
   
   - Une fois dans le fichier YAML retirer les trois lignes de cidr qui sont les étendues ip autorisées

     # Supprimez ceci :
     cidr:
    - "192.168.0.0/16"
    - "10.0.0.0/8"
    - "172.16.0.0/12"

V/ TESTONS CROWDSEC : 

Installer openssh-server si il n'est pas installé : 

# sudo apt install openssh-server

  - Suite à cela vous devez utiliser un autre pc pour testé ici le service SSH, on va requêter à plusieurs reprises et lancer jusqu'à 5 fois la commande :

    # ssh 192.x.x.x

- Vous pourez observer au bout d'un certain nombre de requête que vous ne pourrez pu saisir le mot de passe SSH car votre connexion à était bloqué et détecter par les alertes.

  - Pour voir les alertes détecter :
     # 
