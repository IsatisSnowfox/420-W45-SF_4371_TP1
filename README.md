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

### Vérification du stockage LVM
- `sudo pvs` : vous permet de vérifier l'état de vos physical volumes
- `sudo vgs` : vous permet de vérifier l'état de vos volume groups
- `sudo lvs` : vous permet de vérifier l'état de vos logical volumes

### Vérification de la connexion SSH
Sur votre machine client, tapez la commande `ssh@nom_d_hote_de_votre_serveur -p `

Ensuite, si vous avez configuré votre fichier `~/.ssh/config`, essayez la commande `ssh nom_indique_comme_host` (dans cet exemple, la commande sera `ssh website`)
 