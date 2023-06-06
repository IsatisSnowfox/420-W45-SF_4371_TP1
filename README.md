# ISS_TP1_FG_SB
## Caractérisation de la machine serveur

- Nom de la machine virtuelle et nom de la machine (hostname)
  - VM : E23_4371_420W45_Ub_TP1_SB_2291653
  - Hostname : srv-web-1234567

- Adresses IPv4, IPv6 avec masque et passerelle
  - IPv4 : 10.100.2.196
  - IPv6 : 
  - Masque : 255.255.255.0
  - Passerelle : 10.100.2.1

- Port des services ouverts
  - 

- Usager utilisé pour l'installation
  - 

## Mises à jour préalables à l'installation et ajout de composants nécessaires
Ce que doit contenir votre serveur pour devenir un modèle de déploiement.
- Programmes
  - Nom
    - Version : 
    - Procédure d'installation
    - Répertoires utilisés
      -  Par le programme : 
      -  Par ses fichiers de configuration : 
      -  Par ses données : 
    - Espace disque utilisé :
    - Droits sur les répertoires :
    - Nom d'usager (UID) :
    - Groupe (GID) :

## Procédure de validation de l'installation

### Vérification de l'installation des logiciels de base
- `wget --version` : vérifie votre installation de wget
- `curl --version` : vérifie votre installation de curl
- `git --version` : vérifie votre installation de git
- `docker version` : vérifie votre installation de docker

### Vérification du stockage LVM
- `sudo pvs` : vous permet de vérifier l'état de vos physical volumes
- `sudo vgs` : vous permet de vérifier l'état de vos volume groups
- `sudo lvs` : vous permet de vérifier l'état de vos logical volumes

### Vérification de la connexion SSH
Sur votre machine client, tapez la commande `ssh@nom_d_hote_de_votre_serveur -p `

Ensuite, si vous avez configuré votre fichier `~/.ssh/config`, essayez la commande `ssh nom_indique_comme_host` (dans cet exemple, la commande sera `ssh website`)

Les lignes non commentaire de votre fichier sshd_config devrait ressembler à ça : 
![sshd_config partie 1](img/sshdConfig0.jpg)
![sshd_config partie 2](img/sshdConfig1.jpg)
![sshd_config partie 3](img/sshdConfig2.jpg)

Si vous le souhaitez vous pouvez améliorer la sécurité de votre configuration SSH en vérifiant et modifiant au besoin les lignes suivantes (et en les décommentant si nécessaire) :
- `PermitRootLogin no` &rarr; désactive la connexion via l'utilisateur root
- `PermitEmptyPasswords no` &rarr; Empêche des utilisateurs sans mot de passe de se connecter
- `Port 1234` (ou n'importe quel nombre de votre choix autorisé par votre pare-feu) &rarr; Change le port utilisé par SSH
- `ClientAliveInterval 300` &rarr; configure un délai au bout duquel le client inactif sera déconnecté
- `AllowUsers user1 user2` &rarr; limite l'accès SSH uniquement aux utilisateurs listés
- `AllowGroups ssh_group` &rarr; limite l'accès SSH uniquement aux membres du groupe listé

Pour que les changements soient pris en compte redémarrez le service en utilisant la commande `systemctl restart ssh.service`