---
title: Les OSINTables [1/3]
categories: [404CTF_2023, OSINT_404]
tags: [OSINT]
image: '/assets/images/404CTF_2023/404CTF.jpg'
---

## 𝄞 Introduction

![Intro](/assets/images/404CTF_2023/OSINT/Les_OSINTables_1/intro.png)


## 𝄞 Solution

L'objectif de ce challenge est de **trouver l'adresse d'envoie de la lettre** à l'aide du fichier fourni avec l'énoncé.

![Image](/assets/images/404CTF_2023/OSINT/Les_OSINTables_1/image.png)

En analysant **l'image**, on peut noter plusieurs éléments intéressants :

- **Rue Victor Hugo** : Il s'agit du nom de la rue.
- **VE** : On peut supposer que c'est le début de la ville.
- **Q4** ?
- **LXXXIII** : Il s'agit du chiffre **83** en chiffres romains.

Ma première idée était donc de chercher une adresse commençant par **"83 Rue Victor Hugo VE..."** sur *Google Maps*.

![Maps](/assets/images/404CTF_2023/OSINT/Les_OSINTables_1/maps.png)

J'ai donc essayé chaque possibilité. Dans ce cas, il y a deux résultats possibles : [Vergèze,Versailles]
 

𝄞 FLAG : `404CTF{83_rue_victor_hugo_vergeze}` 𝄞

## 𝄞 Conclusion
Ce challenge **d'OSINT** nous a permis de mettre en pratique nos compétences en recherche d'informations en ligne. En analysant attentivement les indices présents dans l'image fourni, nous avons pu trouver l'adresse de la lettre. L'utilisation d'outils tels que Google Maps s'est avérée utile pour mener à bien cette tâche.





