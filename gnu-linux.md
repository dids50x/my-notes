# GNU/Linux

## Générer un mot de passe aléatoire

```
/dev/urandom tr -dc '1234567890!$%}/?@^`,;:|{*_=#&-abc+defghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ' | head -c12; echo ""
```

---

## Bug mkfs stuck

https://access.redhat.com/solutions/727333

The strace logs for mkfs.xfs or mkfs.ext4 command shows that the command is hanging after issuing the ioctl 0x1277:
Raw
```
        $ tail  -2  mkfs.txt 
        1538  08:59:41.724086 write(1, "\x08\x08\x08\x08\x08\x08\x08\x08\x08\x08\x08\x08\x08", 13) = 13 <0.000053>
        1538  08:59:41.724209 ioctl(3, 0x1277           <-------- hung after this
        [...]
```
From the kernel source, 0x1277 ioctl corresponds to BLKDISCARD:
Raw
```
        include/linux/fs.h:
        ------------------
        344 #define BLKDISCARD _IO(0x12,119)
        [...]
```
```
strace -f -tt -y -T -v -x -o /tmp/mkfs.out -s 4096 mkfs.xfs /dev/mapper/vdo_vol
```

il reste bloqué à ioctl

il faut rajouter l'option '-K' au mkfs (il y a une KB RH pour ça)

---

## Renommer tous les fichiers dans le dossier courant

`rename .repo.bak .repo *`  
ou  
`rename .repo .repo.bak *`

---
