# Quickemu

## Importer une VM Windows 10 VirtualBox dans Quickemu

### Configurer la VM Quickemu cible

Créer la VM cible :
```
quickget windows 10 French
```

Editer le fichier `windows-10-French.conf` et y rajouter les lignes suivantes :
```
tpm="on"
secureboot="off"
boot="legacy"
```

### Configurer la VM VirtualBox source

- Démarrer la VM, puis désinstaller les extensions VirtualBox.
- Si possible, monter l'ISO `virtio-win.iso` présente dans le dossier nouvellement généré de Quickemu pour installer tous les pilotes VirtIO ainsi que les services SPICE.
  Si cette étape n'a pas été effectuée, il sera possible d'ajouter les pilotes à posteriori (voir plus loin).
- Arrêter proprement la VM VirtualBox.

### Convertir l'image du disque dur

```
qemu-img convert -f vdi -O qcow2 yours-machine-name.vdi yours-machine-name.qcow2
```

Remplacer ensuite l'image disque `windows-10-French/disk.qcow2` de la VM Quickemu par l'image disque fraîchement convertie.

### Windows ne démarre plus

Windows ne pourra pas détecter le disque dur `C:` si les pilotes VirtIO ne sont pas présents.  

Premièrement, démarrer la VM à l'aide du DVD d'installation de Windows tout en ayant inséré le CD des pilotes VirtIO :  
- Editer le fichier de configuration de la VM Quickemu (`windows-10-French.conf`) en commentant la ligne `fixed_iso="windows-10-French/virtio-win.iso"` et en rajoutant la ligne `fixed_iso="windows-10-French/windows-10.iso"`. Le but est de monter l'image d'installation de Windows dans `D:`, car QEMU ne peut pas démarrer depuis `E:`.
- Lancer Quickemu avec les arguments suivants pour monter l'image VirtIO et démarrer depuis le DVD d'installation de Windows : `quickemu --vm windows-10-French.conf --extra_args "-drive media=cdrom,index=2,file=windows-10-French/virtio-win.iso -boot order=d"`.

Une fois l'installateur de Windows démarré :  
- Valider l'écran de sélection des langues, cliquer sur `Réparer l'ordinateur` puis sur `Invite de commandes`.
- L'image CD VirtIO doit être assignée au lecteur `E:`. Si ce n'est pas le cas, mettre le bon nom de lecteur dans les commandes suivantes.
- Charger le pilote VirtIO Storage qui permettra à Windows de détecter le disque dur. Ce pilote est chargé à chaud dans l'installateur de Windows (Win RE). Taper `drvload E:\viostor\w10\amd64\viostor.inf`.
- Vérifier que le disque dur est maintenant détecté. Taper `diskpart`, puis `list disk`. Le *Disque 0* de la taille attendue doit maintenant apparaître et son statut doit être *en ligne*.
- Taper `list volume` pour déterminer quel est le nom de volume temporaire correspondant au volume `C:` du disque dur. Dans l'exemple suivant, ce sera `F:`. Taper `exit` pour quitter `diskpart`.
- Installer le pilote VirtIO Storage sur le disque dur. Pour cela, taper `dism /image:F:\ /add-driver:E:\viostor\w10\amd64\viostor.inf`.
- Arrêter la machine virtuelle proprement.

Editer à nouveau le fichier de configuration de la VM Quickemu (`windows-10-French.conf`) en commentant la ligne `fixed_iso="windows-10-French/windows-10.iso"` et en décommentant la ligne `fixed_iso="windows-10-French/virtio-win.iso"` pour que l'image CD VirtIO soit montée au prochain démarrage de Windows.  

Enfin, démarrer la VM Windows normalement, puis installer tous les pilotes VirtIO depuis le CD, ainsi que les services SPICE.
