# Commandes Linux pour les vieux Macintosh

## Désarchiver une archive StuffIt (.sit) sous Linux

Installer le paquet Debian `unar` et taper `unar <archive.sit>`.

La commande `unar` fonctionne aussi pour les fichiers `.bin` créés avec StuffIt ou Disk Copy.

Attention : tout le contenu de l'archive est extrait sous Linux, ce qui sépare les fichiers `.rsrc` des autres fichiers. MacOS n'est ensuite plus capable de reconnaître les autres fichiers car ils ne correspondent plus qu'à de la donnée brute (par exemple, des extensions système).
Si possible, il vaut mieux installer StuffIt Expander sur MacOS et extraire les archives directement sur MacOS.

## Afficher le contenu d'une archive StuffIt (.sit) sous Linux

```
lsar -L <archive.sit>
```

## Convertir une archive StuffIt (.sit) récente en une version plus ancienne

Utiliser StuffIt Deluxe 5.5 pour désarchiver l'archive récente, puis StuffIt Lite 3.6 pour l'archiver à nouveau dans un format plus ancien.

Le site web [ReStuff 2](https://restuff.jcs.org/) permet d'automatiser cette procédure.

## Convertir une image DMG en image CD Apple sous Linux

Sous Debian, installer le paquet `dmg2img` et taper `dmg2img <image.dmg>`.
L'image résultante est une image CD Apple, l'équivalent d'une image ISO.
