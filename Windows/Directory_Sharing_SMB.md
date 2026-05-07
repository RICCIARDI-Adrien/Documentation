# Partage de dossiers via SMB

## Accès non authentifié sous Windows 11

Si l'erreur *Accès invité non authentifié* surgit sous Windows 11, activer la connexion non sécurisée.  
Lancer PowerShell en mode administrateur et taper :
```
Set-SmbClientConfiguration -EnableInsecureGuestLogons $true -Force
```

Source : https://learn.microsoft.com/en-us/windows-server/storage/file-server/enable-insecure-guest-logons-smb2-and-smb3

## Connexion du lecteur réseau

* Ouvrir l'explorateur de fichiers.
* Cliquer droit sur **Ce PC**, puis choisir **Connecter un lecteur réseau**.
* Pour Quickemu, taper l'adresse de dossier `\\10.0.2.4\qemu`.

Source : https://support.microsoft.com/en-us/windows/file-sharing-over-a-network-in-windows-b58704b2-f53a-4b82-7bc1-80f9994725bf
