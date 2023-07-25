---
title: 48 Meters Underground
categories: [leHACK_2023, IoT_leHACK]
tags: [IoT, binwalk]
image: '/assets/images/leHACK_2023/leHACK.jpg'
---

## 𝄞 Introduction
![Analyse](/assets/images/leHACK_2023/IoT/48_Meters_Underground/intro.png)

## 𝄞 Solution

Pour résoudre ce défi, j'ai commencé par analyser le fichier fourni en utilisant plusieurs outils. J'ai rapidement constaté que l'outil **binwalk** avait détecté un système de fichiers **Squashfs**. Ce format est souvent utilisé dans les systèmes d'exploitation embarqués tels que les routeurs, les périphériques de stockage en réseau ou les objets IoT.

![Analyse](/assets/images/leHACK_2023/IoT/48_Meters_Underground/analyses.png)

J'ai extrait le système de fichiers Squashfs en utilisant la commande suivante :

```shell
binwalk -e firmeware.bin
```
En explorant le dossier **"squashfs-root"**, j'ai découvert une structure de fichiers correspondant à un système Linux (ce qui est logique). Ma première idée a été de rechercher des fichiers de configuration, des clés SSH, des mots de passe, etc.

![Squashfs](/assets/images/leHACK_2023/IoT/48_Meters_Underground/squashfs.png)


![Telnet](/assets/images/leHACK_2023/IoT/48_Meters_Underground/telnet.png)

Comme on peut le voir, nous trouvons un script shell de configuration **telnet** où nous trouvons le nom d'utilisateur *Device_Admin* et le mot de passe stocké dans la variable *$sign*, qui correspond à **/etc/config/sign**. 


Si nous examinons ce fichier où le mot de passe est censé être stocké...

![Flag](/assets/images/leHACK_2023/IoT/48_Meters_Underground/flag.png)


𝄞 FLAG : `leHACK{w4ll_h1dd3n_p13c3_<-_->}` 𝄞 


## 𝄞 Conclusion
En conclusion, j'ai réussi à résoudre le défi "48 Meters Underground" en analysant le fichier fourni et en extrayant le système de fichiers Squashfs. En explorant les fichiers du système, j'ai finalement découvert le flag recherché.




