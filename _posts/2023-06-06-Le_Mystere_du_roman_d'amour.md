---
title: Le Mystère du roman d'amour
categories: [404CTF_2023, Forensic]
tags: [swp,Steganographie]
---

## 𝄞 Introduction

![Intro](/assets/images/404CTF_2023/Forensic/Le_Mystere_du_roman_d'amour/intro.png)


Nous disposons d'un fichier au format **swp** à analyser.

## 𝄞 Fichier swp
Tout d'abord, qu'est-ce qu'un **fichier swp** ? Les fichiers de swap Vim, également connus sous le nom de fichiers swp, sont des fichiers temporaires créés par l'éditeur de **texte Vim** lors de l'édition d'un fichier. Ils servent à stocker les modifications **non sauvegardées** en cas de fermeture anormale du programme, de panne du système ou d'autres interruptions inattendues.

## 𝄞 Solution
La première étape consiste à **analyser le fichier .swp** pour obtenir des informations. Pour cela, nous allons utiliser **la commande file** :

```bash
  file fichier-etrange.swp 𝄞
```

![File](/assets/images/404CTF_2023/Forensic/Le_Mystere_du_roman_d'amour/file.png)

Nous obtenons plusieurs informations :
 - Le PID : 168
 - L'utilisateur : jaqueline
 - Le nom de la machine : aime_ecrire
 - Le chemin relatif du fichier : ~jaqueline/Documents/Livres/404 Histoires d'Amour pour les bibliophiles au cœur d'artichaut/brouillon.txt


Ensuite, nous allons essayer de **récupérer** le contenu du fichier **.swp** en utilisant la commande suivante :

```bash
  vim -r fichier-etrange.swp
```

*Lorsque vous exécutez la commande **"vim -r file.swp"**, Vim essaie de récupérer les données du fichier de swap spécifié (dans ce cas, "fichier-etrange.swp") et les intègre dans un fichier de sauvegarde.*

![Vim](/assets/images/404CTF_2023/Forensic/Le_Mystere_du_roman_d'amour/vim.png)

En examinant le contenu de ce fichier de sauvegarde dans Vim, nous remarquons rapidement qu'il s'agit d'une **image** avec la signature **PNG** et le chunck **IHDR**. Pour l'enregistrer, nous utilisons la commande suivante directement dans vim.

```bash
  :w flag.png dans Vim.
```

![Book](/assets/images/404CTF_2023/Forensic/Le_Mystere_du_roman_d'amour/book.png)

À première vue, l'image semble ordinaire, mais nous soupçonnons l'utilisation d'une technique de stéganographie pour cacher des données.

Après avoir utilisé les outils classiques de stéganographie tels que *Exiftool*, *Strings*, *Pngcheck*, *etc*, je décide d'utiliser l'outil **Stegsolve** pour explorer les filtres de couleur. Le filtre **Blue Plane 0** nous renvoie une image qui ressemble à un **QR Code**.

![Stegsolve](/assets/images/404CTF_2023/Forensic/Le_Mystere_du_roman_d'amour/qrcode_stegsolve.png)

Nous pouvons extraire le contenu de ce QR Code avec ce [site](https://products.aspose.app/barcode/recognize/qr#)

![Flag](/assets/images/404CTF_2023/Forensic/Le_Mystere_du_roman_d'amour/flag.png)

Nous avons maintenant toutes les informations pour résoudre ce challenge ! 

𝄞 FLAG : `404CTF{168-~jaqueline/Documents/Livres/404 Histoires d'Amour pour les bibliophiles au coeur d'artichaut/brouillon.txt-jaqueline-aime_ecrire-3n_V01L4_Un_Dr0l3_D3_R0m4N}` 𝄞

## 𝄞 Conclusion
Nous avons analysé un fichier **.swp** créé par l'éditeur Vim. En utilisant différentes commandes et outils, nous avons pu extraire une image cachée dans le fichier et appliquer des techniques de stéganographie pour révéler un **QR Code**. Ce QR Code nous a finalement fourni la dernière parti du flag. Cette résolution a démontré l'importance de l'analyse approfondie des fichiers et l'utilisation de techniques spécialisées pour découvrir des informations cachées.

