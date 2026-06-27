# Configurer le fuseau horaire en ligne de commande

La définition du fuseau horaire depuis l'interface graphique des paramètres impose maintenant d'activer le service de localisation du Mac.

Cependant, forcer le fuseau horaire depuis la ligne de commande évite d'activer le service de localisation.

## Lister les fuseaux horaires disponibles

```
sudo systemsetup -listtimezones
```

## Définir un fuseau horaire

```
sudo systemsetup -settimezone Europe/Paris
```
