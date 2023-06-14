---
title: Note de bas de page
categories: [404CTF_2023, Forensic]
tags: [Autopsy,aCropalypse]
---

## 𝄞 Introduction

![Intro](/assets/images/404CTF_2023/Forensic/Note_de_bas_de_page/intro.png)

Nous disposons d'un fichier au format **.pst** à analyser.

## 𝄞 Fichier pst

Un fichier **.pst** est l'abréviation de *Personal Storage Table (Tableau de stockage personnel)*, est un format de fichier utilisé par le logiciel de messagerie **Microsoft Outlook** pour stocker des données telles que les e-mails, les contacts, les calendriers et autres informations personnelles.

## 𝄞 Solution

Pour analyser ce fichier, j'ai utilisé le logiciel **Autopsy** sur Windows. Nous aurions également pu utiliser **Outlook pst viewer**.

![Mail](/assets/images/404CTF_2023/Forensic/Note_de_bas_de_page/mail.png)

Comme nous pouvons le voir, nous avons trouvé 12 images et 5 e-mails.

En examinant les e-mails, nous avons découvert un e-mail très intéressant :

![Voltaire](/assets/images/404CTF_2023/Forensic/Note_de_bas_de_page/voltaire.png)

Cet e-mail est accompagné d'une capture d'écran.

![capture](/assets/images/404CTF_2023/Forensic/Note_de_bas_de_page/capture.png)

Aaarh ! Il n'y a que le début du flag. Je commence par effectuer une analyse basique de cette image.

En utilisant *Exiftool* et *pngcheck*, nous remarquons quelque chose d'intéressant :

![Exiftool](/assets/images/404CTF_2023/Forensic/Note_de_bas_de_page/exiftool.png)

Il y a des données après le **chunk IEND**, qui marque normalement la fin de l'image. 
Je décide donc d'approfondir mes investigations et d'examiner **l'image en hexadécimal**.

![IEND1](/assets/images/404CTF_2023/Forensic/Note_de_bas_de_page/IEND1.png)
![IEND2](/assets/images/404CTF_2023/Forensic/Note_de_bas_de_page/IEND2.png)

Nous remarquons également la présence de **deux chunks IEND**, ce qui est encore moins normal. En effet, une image **PNG** est constituée d'un *chunk IHDR*, de plusieurs *chunks IDAT* et d'un *chunk IEND*. Nous avons donc la confirmation qu'il y a un problème avec cette image. J'ai alors testé plusieurs techniques de stéganographie pour essayer de révéler ces données supplémentaires, mais sans succès. Après plusieurs jours de blocage, je décide d'explorer une autre piste et c'est là que je remarque que l'image est **"recadrée"**, comme si elle avait été volontairement tronquée. Je me pose alors la question suivante :

### 𝄞𝄞 Est-il possible de récupérer l'image originale à partir d'une image recadrée ?

Je commence à effectuer des recherches et je tombe sur un article très récent [site](https://korben.info/acropalypse-faille-png.html). Cette faille permet de récupérer des données à partir de fichiers **PNG** qui ont été recadrés. Cela concerne principalement les smartphones **Google Pixel**, ça pourrait resembler avec que l'on a mais ici il s'agit d'une image recadrée sur un système Windows et non pas sur un Google Pixel alors je poursuis mes recherches et je trouve ceci :

![Windows](/assets/images/404CTF_2023/Forensic/Note_de_bas_de_page/windows.png)

Je trouve rapidement le script de la **PoC** [site](https://gist.github.com/DavidBuchanan314/93de9d07f7fab494bcdf17c2bd6cef02). Il suffit de modifier le script pour qu'il prenne en charge les images **RGBA** au lieu de **RGB**. Une fois le script modifié, je le teste et j'obtiens cette image.

```python
python acropalypse_png.py restore windows "Capture d’écran 2023-05-07 210840.png" restore.png
```

![Flag](/assets/images/404CTF_2023/Forensic/Note_de_bas_de_page/flag.png)

𝄞 FLAG : `404CTF{L3_f0rM1d@bl3_p09re35_d3s_lUm13re5}` 𝄞

## 𝄞 Conclusion

En analysant un fichier **pst** avec Autopsy, nous avons découvert une image suspecte dans un e-mail qui était accompagnée d'une capture d'écran. Après avoir examiné de près cette image, nous avons constaté des anomalies, telles que la présence de données après le chunk IEND et la présence de deux chunks IEND, ce qui est atypique pour un fichier PNG. Après avoir exploré différentes techniques de stéganographie sans succès, nous avons envisagé la possibilité de récupérer l'image originale à partir d'une image recadrée. Après des recherches approfondies, nous avons trouvé une faille récente dans le format **PNG** qui permet de récupérer des données à partir d'images recadrées, bien que cette faille soit principalement présente sur les smartphones Google Pixel. Cependant, grâce à une solution adaptée à notre situation sous Windows, nous avons réussi à récupérer l'image originale, révélant ainsi le flag tant recherché.

