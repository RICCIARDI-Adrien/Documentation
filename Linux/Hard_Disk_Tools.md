# Outils d'analyse de l'occupation des disques

* Avec interface graphique : `Baobab`
* En ligne de commande : `ncdu`

Les deux programmes sont disponibles dans les dépôts Debian.

# Nettoyer un SSD

Démarrer la machine sur une image externe pour avoir un accès complet au SSD à effacer.

Effacer tous les blocs à la main :
```
sudo dd if=/dev/zero of=/dev/<disque dur> bs=4M status=progress
```

Trimmer les blocs :
```
sudo blkdiscard --secure --verbose /dev/<disque dur>
```

L'option `--secure` n'est peut-être pas disponible sur tous les contrôleurs de SSD.

# Smartctl pour les SSD

Installer le paquet `nvme-cli` (testé sous Debian 13).

* Voir la liste des périphériques disponibles : `sudo nvme list`
* Afficher les statistiques SMART : `sudo nvme smart-log -v <périphérique, par ex. /dev/nvme0n1>`
