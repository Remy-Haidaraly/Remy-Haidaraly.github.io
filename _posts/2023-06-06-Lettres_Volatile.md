---
Titre : Lettres Volatiles
categories: [404CTF_2023, Forensic_404]
tags: [Volatility]
---
## 𝄞 Introduction

![Intro](/assets/images/404CTF_2023/Forensic/Lettres_volatiles/intro.png)

Nous avons à notre disposition un fichier au format **zip** à analyser.

## 𝄞 Fichier Zip

Le fichier **zip** contient plusieurs fichiers.

![Files](/assets/images/404CTF_2023/Forensic/Lettres_volatiles/files.png)


Notre objectif est d'extraire le contenu du fichier **.zip** qui est protégé par un mot de passe. Il existe différentes méthodes pour "cracker" ou "brute-forcer" le mot de passe d'un fichier **.zip**, mais cela n'est pas l'objectif de ce défi.

## 𝄞 Solution

J'ai rapidement repéré le fichier **.zip** protégé par mot de passe, situé dans le répertoire ***/C311M1N1/Documents/perso/s3cR37.zip***.

J'ai également trouvé un fichier **.raw** très intéressant dans le répertoire ***/C311M1N1/Documents/JumpBag/C311M1N1-PC-20230514-200525.raw***.

Le titre du défi, *"Lettres Volatiles"*, m'a fait pensé à l'outil **Volatility**, qui permet d'analyser des dumps de mémoire. J'ai donc décidé d'utiliser **Volatility** sur le fichier **.raw**.

*J'ai utilisé Volatility sur Windows, mais il est également possible de réaliser les mêmes étapes sur Linux.*

### 𝄞𝄞 Volatility 
Notre premier objectif est de déterminer le **profil de l'image** en exécutant la commande suivante :

```bash
volatility.exe -f C311M1N1-PC-20230514-200525.raw imageinfo
```

![imageinfo](/assets/images/404CTF_2023/Forensic/Lettres_volatiles/imageinfo.png)

Le profil correspondant à notre image est généralement **le premier que nous propose Volatility**, donc le profil est **Win7SP1x64**.

Maintenant que nous avons le profil, nous pouvons utiliser différentes commandes et plugins pour interagir avec cette image. Ayant une grande affection pour **Volatility**, j'ai immédiatement pensé à utiliser la commande **clipboard** pour vérifier s'il y avait du texte dans la mémoire du presse-papiers.

```bash
volatility.exe -f C311M1N1-PC-20230514-200525.raw --profile=Win7SP1x64 clipboard
```

![clipboard](/assets/images/404CTF_2023/Forensic/Lettres_volatiles/clipboard.png)

Nous avons ainsi obtenu le mot de passe du fichier **.zip** : *'F3eMoBon8n3GD5xQ'*.

À l'intérieur du fichier **.zip**, Il y a un fichier **PDF** contenant le flag à la fin !

![flag](/assets/images/404CTF_2023/Forensic/Lettres_volatiles/flag.png)

𝄞 FLAG : `404CTF{V0147i1I7y_W1Ll_N3v3r_Wr8_loV3_l3ttEr5}` 𝄞

## 𝄞 Conclusion

Grâce à l'analyse du fichier **.raw** à l'aide de l'outil **Volatility**, nous avons pu extraire le mot de passe du
fichier **.zip** et obtenir le flag caché à l'intérieur d'un fichier PDF. Ce défi mettait en avant l'importance de l'analyse de la mémoire volatile pour la résolution de problèmes de forensic.
