# Réinitialiser un mot de passe utilisateur

Testé sous Windows 10 avec Ubuntu 22.04.

1. Démarrer avec le live CD.
2. Ajouter le support du dépôt `universe` pour avoir accès au programme de manipulation du SAM Windows :
   1. Editer le fichier `/etc/apt/sources.list` et rajouter `universe` à la seconde URL.
   2. Exécuter `sudo apt update`.
3. Installer `chntpw` : `sudo apt install chntpw`.
4. Monter la partition Windows.
5. Ouvrir un terminal, se rendre dans le point de montage de la partition Windows, puis dans le dossier `Windows/System32/config`.
5. Taper `sudo chntpw -l SAM` pour lister les utilisateurs.
6. Taper `sudo chntpw -i SAM` pour passer en mode édition.
   1. Choisir le menu `1. Edit user data and passwords`.
   2. Mettre le RID du compte à modifier.
   3. Choisir le menu `1. Clear`.
   4. Quitter en sauvegardant.
7. Rebooter sous Windows.

Source : https://opensource.com/article/18/3/how-reset-windows-password-linux
