---
title: Une partition endommagé
categories: [m1ndbr34k_2025, Steganographie_m1ndbr34k_2025]
tags: [Steganographie]  
image: '/assets/images/m1ndbr34k/logo.png'
---

## 𝄞 Introduction

![ntro](/assets/images/m1ndbr34k_2025/Steganographie/Une_partition_endommage/intro.png)

---

![img](/assets/images/m1ndbr34k_2025/Steganographie/Une_partition_endommage/image.webp)

L’image fournie est corrompue. L’objectif du joueur est donc de la réparer afin d’y découvrir le flag. Ce challenge vise à initier l’utilisateur au fonctionnement d’une image PNG.


## 𝄞𝄞 Solution
L’utilisation d’**exiftool** ou de la commande **file** permet de détecter rapidement une anomalie au niveau de l’image, indiquant qu’elle est **corrompue**.

![exiftool](/assets/images/m1ndbr34k_2025/Steganographie/Une_partition_endommage/exiftool.webp)

Pour résoudre ce challenge, il est essentiel de comprendre la structure d’un fichier **PNG**. Ce type de fichier débute systématiquement par une séquence de **8 octets** appelée *magic bytes*, qui permet d’identifier le format. Ensuite, le fichier est constitué d’une série de blocs (ou chunks) bien définis, parmi lesquels les plus courants sont *IHDR*, *IDAT* et *IEND*. Chacun de ces chunks joue un rôle précis dans la définition et l’affichage de l’image.

## Image corrompue  en hexa
Si nous examinons l’image corrompue en hexadécimal

![Hexa](/assets/images/m1ndbr34k_2025/Steganographie/Une_partition_endommage/hexa.webp)

On remarque certaines incohérences (encadrées en bleu) qui sont à l’origine de la corruption du fichier. En consultant rapidement la structure d’un fichier **PNG** sur Internet, on comprend que ces erreurs empêchent le bon traitement de l’image.


![png](/assets/images/m1ndbr34k_2025/Steganographie/Une_partition_endommage/png.webp)

![correction](/assets/images/m1ndbr34k_2025/Steganographie/Une_partition_endommage/correction.webp)

Il suffit alors de corriger ces incohérences pour restaurer l’image et ainsi révéler son contenu.

![partition](/assets/images/m1ndbr34k_2025/Steganographie/Une_partition_endommage/partition.webp)

𝄞 FLAG : `MB{v1v3_l3_f0rm47_png}`𝄞
