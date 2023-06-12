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

- Fichiers hosts
![Fichiers hosts](img/fichierHosts.jpg)

- Port des services ouverts
  - **systemd-n :** 68
  - **systemd-r :** 53
  - **sshd :** 22
  - **mysqld :** 3306, 33060
  - **nginx :** 80
  ![Ports des services ouverts](img/PortsUtilises.jpg)

- Usager utilisé pour l'installation
  - **Nom d'utilisateur :** ldubois
  - **Mot de passe :** password

## Mises à jour préalables à l'installation et ajout de composants nécessaires
Ce que doit contenir votre serveur pour devenir un modèle de déploiement.

Avant de commencer l'installation de nouveaux packages, mettre à jour les packages existants en utilisant les commandes suivantes :

`sudo apt update && sudo apt full-upgrade -y`

- Programmes
  - wget
    - Version : 1.21.2
    - Procédure d'installation : `apt install wget`
    - Répertoires utilisés
      -  Par le programme : /usr/bin/wget
      -  Par ses fichiers de configuration : /etc/wgetrc 
      -  Par ses données : /etc/wgetrc 
    - Espace disque utilisé : 516K
    - Droits sur les répertoires : rwxr-xr-x
    - Nom d'usager (UID) : root
    - Groupe (GID) : root
  - git
    - Version : 2.34.1
    - Procédure d'installation : `apt install git`
    - Répertoires utilisés
      -  Par le programme : /usr/bin/git/
      -  Par ses fichiers de configuration : N/A 
      -  Par ses données : N/A 
    - Espace disque utilisé : 3.6M
    - Droits sur les répertoires : rwxr-xr-x 
    - Nom d'usager (UID) : root
    - Groupe (GID) : root
  - curl
    - Version : 7.81.0
    - Procédure d'installation : `apt install curl`
    - Répertoires utilisés
      -  Par le programme : /usr/bin/curl
      -  Par ses fichiers de configuration : N/A
      -  Par ses données : N/A
    - Espace disque utilisé : 255K
    - Droits sur les répertoires : rwxr-xr-x
    - Nom d'usager (UID) : root
    - Groupe (GID) : root
  - docker
    - Version : 24.0.2
    - Procédure d'installation ([Installation de docker](https://get.docker.com/)) : 
      1. Téléchargez le script 
         - `curl -fsSL https://get.docker.com -o install-docker.sh`
      2. Lancez le script en sudo
         - `sudo sh install-docker.sh`   
    - Répertoires utilisés
      -  Par le programme : /usr/bin/docker
      -  Par ses fichiers de configuration : /etc/docker/
      -  Par ses données : /etc/docker/ 
    - Espace disque utilisé : 4.0K
    - Droits sur les répertoires : rwxr-xr-x
    - Nom d'usager (UID) : root
    - Groupe (GID) : root
  - nginx
    - Version : 1.18.0
    - Procédure d'installation : 
    - Répertoires utilisés
      -  Par le programme : /usr/sbin/nginx 
      -  Par ses fichiers de configuration : /etc/nginx/
      -  Par ses données : /etc/nginx/
    - Espace disque utilisé : 4.0K
    - Droits sur les répertoires : rwxr-xr-x
    - Nom d'usager (UID) : root
    - Groupe (GID) : root
  - mysql server
    - Version : 8.0.33-0
    - Procédure d'installation : `sudo apt install mysql-server-8.0 && sudo mysql_secure_installation`
    - Répertoires utilisés
      -  Par le programme : /usr/bin/mysql 
      -  Par ses fichiers de configuration : /etc/mysql/
      -  Par ses données : /etc/mysql/
    - Espace disque utilisé : 6.7M
    - Droits sur les répertoires : rwxr-xr-x
    - Nom d'usager (UID) : root
    - Groupe (GID) : root

  - php
    - Version : 8.1.2-1
    - Procédure d'installation : `sudo apt install php-fpm php-cli php-mysql php-curl php-json`
    - Répertoires utilisés
      -  Par le programme : /usr/bin/php 
      -  Par ses fichiers de configuration : /etc/8.1/
      -  Par ses données : /etc/php8.1/
    - Espace disque utilisé : 5.3SM
    - Droits sur les répertoires : rwxr-xr-x
    - Nom d'usager (UID) : root
    - Groupe (GID) : root

## Procédure de validation de l'installation

### Vérification de l'installation des logiciels de base
- `wget --version` : vérifie votre installation de wget
- `curl --version` : vérifie votre installation de curl
- `git --version` : vérifie votre installation de git
- `docker version` : vérifie votre installation de docker
- `nginx -v` : vérifie votre installation de nginx
- `mysql --version` : vérifie votre installation de mysql
- `php --version` : vérifie votre installation php

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

Il existe également d'autres outils de sécurité tels que Fail2Ban et Google Authenticator qui peuvent protéger contre les attaques par force brute et mieux sécuriser les connexions.

En plus, vous pouvez activer les connexions basées sur des clés SSH. Pour ce faire, il faut créer un fichier "authorized_keys" sur le serveur et puis mettre toutes les clés SSH publiques des ordinateurs autorisés dedans. Ensuite, changez `PasswordAuthentication Yes` pour `PasswordAuthentication Yes`, assurez-vous que la ligne `PubkeyAuthentication yes` est activée et que votre fichier "authorized_keys" est identifié dans la ligne `AuthorizedKeysFile`.

Pour que les changements soient pris en compte redémarrez le service en utilisant la commande `systemctl restart ssh.service`
