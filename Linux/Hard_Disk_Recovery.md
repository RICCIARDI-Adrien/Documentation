# Récupérer les données d'un disque dur

## Paquets Debian nécessaires

Installer les paquets suivants :

```
sudo apt install gddrescue kpartx testdisk
```

## Extraire les données du disque physique

* Brancher le disque à récupérer et éventuellement démonter son système de fichiers s'il se monte automatiquement.
* Lancer la commande `sudo ddrescue -vv /dev/sdc /media/ar/Elements1To/disque.img ~/Bureau/journal`.
  * `/dev/sdc` est le disque à récupérer.
  * `/media/ar/Elements1To/disque.img` correspond à l'image disque qui va être créée.
  * `~/Bureau/journal` est le fichier journal consignant le déroulement de la lecture du disque à récupérer (cela peut servir en cas d'erreur de lecture).
* Faire une copie de sécurité de l'image récupérée avant de risquer de la modifier : `cp /media/ar/Elements1To/disque.img /media/ar/Elements1To/disque.img.bak`.

## Trouver les partitions

* Lancer la commande `testdisk /log /debug /media/ar/Elements1To/disque.img` et suivre les instructions.
* Réécrire la table des partitions dans l'image `disque.img` si nécessaire.

## Accéder aux partitions

* Lancer la commande `sudo kpartx -a -v /media/ar/Elements1To/disque.img` pour créer un device simulant un disque dur contenant l'image disque.
* Si la commande ne retourne rien, c'est que la table des partitions est invalide.

## Réparer le système de fichiers

* Utiliser `testdisk disque.img` pour vérifier l'état de la partition. Il est aussi possible de récupérer quelques fichiers grâce à la commande de copie des fichiers trouvés.
* TODO (peut-être VM sous windows avec comme disque un /dev/mapper/loop... pour passer le vrai chkdsk)
* Monter chaque partition avec la commande `sudo mount /dev/mapper/loop0p1 /mnt`.
  * `/dev/mapper/loop0p1` correspond à une partition, il faut aussi changer le point de montage à chaque fois.

## Récupérer des fichiers

* Si le système de fichiers ne peut être monté, tiliser la commande `photorec /debug /log /d <recup_dir> <image_disque>`.
  * `recup_dir` est le dossier dans lequel seront placés tous les fichiers récupérés.
  * `image_disque` est l'image disque récupérée avec `ddrescue`.

## Divers

Sous Debian 7, installer les paquets suivants :
```
smartmontools
sg3-utils
```

Test SMART : http://blog.shadypixel.com/monitoring-hard-drive-health-on-linux-with-smartmontools/
Récupération des blocs endommagés : http://smartmontools.sourceforge.net/badblockhowto.html#bb

http://www.thomas-krenn.com/en/wiki/Analyzing_a_Faulty_Hard_Disk_using_Smartctl
