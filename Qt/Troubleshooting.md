# Astuces de dépannage Qt

## Linux

### Les dialogues sont extrêmement lents

Les dialogues standards de Qt (et KDE) mettent plusieurs secondes à s'ouvrir et à se fermer.

Solution trouvée sous Debian 13 : le fichier `~/.config/QtProject.conf` pèse 512Mo car un des chemins dans la propriété `shortcuts` est beaucoup trop long (c'était un chemin contenant des caractères accentués, lesquels étaient répétés des millions de fois).  
Supprimer le fichier a résolu le problème.