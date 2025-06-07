---
title: La composition perdue du pianiste
categories: [m1ndbr34k_2025, Forensic_m1ndbr34k_2025]
tags: [Forensic]  
image: '/assets/images/m1ndbr34k/logo.png'
---

## 𝄞 Introduction

![Intro](/assets/images/m1ndbr34k_2025/Forensic/La_composition_perdue_du_pianiste/intro.png)
---

## 𝄞𝄞 Solution 

On commence par regarder les fichiers sur le Desktop de l’utilisateur.

```python
python2 vol.py -f /home/kali/Desktop/medium.mem --profile=Win7SP1x86_23418 filescan | grep "Desktop"
```
![vol1](/assets/images/m1ndbr34k_2025/Forensic/La_composition_perdue_du_pianiste/vol.webp)

On trouve un fichier appelé "**partition_secrete.rar** nous pouvons extraire ce fichier avec la commande suivante : 

```python
python2 vol.py -f /home/kali/Desktop/medium.mem --profile=Win7SP1x86_23418 dumpfiles -Q 0x000000003f8aff80 -D /home/kali/Desktop
```

![vol2](/assets/images/m1ndbr34k_2025/Forensic/La_composition_perdue_du_pianiste/vol2.webp)

Nous pouvons essayer d’extraire le fichier **.rar**

![rar](/assets/images/m1ndbr34k_2025/Forensic/La_composition_perdue_du_pianiste/rar.webp)

Mais on nous demande un mot de passe … il faut aller chercher dans la ram un mot de passe pour pouvoir extraire le contenu du fichier **.rar**

La commande **clipboard**, nous renvoie une chaine encodé en **base64**

```python
 python2 vol.py -f /home/kali/Desktop/medium.mem --profile=Win7SP1x86_23418 clipboard
 ```
![clipboard2](/assets/images/m1ndbr34k_2025/Forensic/La_composition_perdue_du_pianiste/clipboard2.webp)

Qui une fois décodé, affiche un rabbit hole.

![rabbit](/assets/images/m1ndbr34k_2025/Forensic/La_composition_perdue_du_pianiste/rabbit.webp)

Il va falloir chercher plus loin. 

## Historique navigateur

Pour trouver le mot de passe du fichier **.rar**, il va falloir fouiller côté historique du navigateur.

```python
python2 vol.py -f /home/kali/Desktop/medium.mem --profile=Win7SP1x86_23418 iehistory
```
![rabbit](/assets/images/m1ndbr34k_2025/Forensic/La_composition_perdue_du_pianiste/pastebin.webp)

On trouve un lien [Pastebin](https://pastebin.com/CJax0v8Q) Note à moi même : Le mot de passe de mon zip est : fxoverflo…

![password](/assets/images/m1ndbr34k_2025/Forensic/La_composition_perdue_du_pianiste/password.webp)

Nous avons maintenant le mot de passe  du fichier **.rar**

Nous obtenons un fichier "**wordlist.txt**" et un fichier "**flag2.png**"

![partition](/assets/images/m1ndbr34k_2025/Forensic/La_composition_perdue_du_pianiste/partition.webp)

On trouve le code secret pour le flag2 : **m0z4r7**. Il nous manque plus qu’a trouver le mot de passe de l’utilisateur.

## Mot de passe du compte “Le Pianiste”

Quand on regarde le fichier **wordlist.txt**.

![wordlist](/assets/images/m1ndbr34k_2025/Forensic/La_composition_perdue_du_pianiste/wordlist.webp)

On tombe sur une belle wordlist de mot de passe. Il va falloir utiliser le plugin “**hashdump**” de  **volatility3** ou utiliser **hivedump** de **volatility2** pour dump la table *SAM* et *SYSTEM*. 

```python
python3 vol.py -f /media/sf_Share_folder/medium.mem windows.hashdump
```
![hashdump](/assets/images/m1ndbr34k_2025/Forensic/La_composition_perdue_du_pianiste/hashdump.webp)

Voici le hash du compte "*Le-Pianiste*" : **`235118796ff07ea2c26380053f06d9b2`**

Nous pouvons maintenant essayer de le casser avec notre wordlist !

```shell
hashcat -m 1000 hash.txt wordlist.txt
```
![crack](/assets/images/m1ndbr34k_2025/Forensic/La_composition_perdue_du_pianiste/crack.webp)

Nous avons maintenant le flag au complet ! 

 𝄞 FLAG : `MB{b1aab836-bef5-42b5-bf02-955913fd18e6}`𝄞
