# Utilitaire socat

## Créer un tunnel port série vers TCP

```
socat /dev/ttyS0,raw,b19200,echo=0 tcp4-listen:1234
```

## Créer un tunnel port série vers TCP persistant

Ce tunnel survit à la déconnexion de l'utilisateur qui l'a créé ainsi qu'à la déconnexion du client TCP.

```
nohup socat /dev/ttyUSB0,raw,b19200,echo=0 tcp4-listen:1234,fork > /dev/null &
```
