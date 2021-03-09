# GNU/Linux

## Générer un mot de passe aléatoire

```
/dev/urandom tr -dc '1234567890!$%}/?@^`,;:|{*_=#&-abc+defghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ' | head -c12; echo ""
```
