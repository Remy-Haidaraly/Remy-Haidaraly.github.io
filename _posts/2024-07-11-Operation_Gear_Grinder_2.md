---
title: Operation Gear Grinder - Sur écoute 2/12
categories: [Shutlock-CTF_2024, Osint_shutlock]
tags: [Osint]
image: '/assets/images/Shutlock-ctf_2024/logo.jpg'
---

## 𝄞 Introduction

![Intro](/assets/images/Shutlock-ctf_2024/Osint/Operation_Gear_Grinder-Signalement_2_12/intro.png)

## 𝄞 Solution

Nous avons à notre disposition un fichier **.mp3**. À partir de ce fichier audio, nous devons trouver l'identité d'un athlète de haut niveau ainsi que le nom d'une molécule naturellement produite par le corps qui a été détectée à deux reprises lors de tests sur cet athlète.

En écoutant cet audio, nous apprenons plusieurs choses sur cet athlète :

Informations sur l'athlète inconnu : 

1. Aussi vieux que la Renault 16
2. Plus petit que **Christophe Durandier** (en taille <180 cm)
3. Son pays de naissance a accueilli l'Eurovision
4. Il est banni pour les 35-40 prochaines années
5. Un site parle de cette histoire, ce site a un logo qui ressemble à celui d'Île-de-France Mobilités

À partir de ces informations, nous pouvons identifier l'athlète.

## 𝄞 Méthodologie 

Premièrement, nous allons regarder la date de sortie de la **Renault 16** :

Renault 16 --> 1965
![Renault](/assets/images/Shutlock-ctf_2024/Osint/Operation_Gear_Grinder-Signalement_2_12/renault.png)

Ensuite, nous cherchons le pays qui a été l'hôte de l'Eurovision en 1965 ! Une petite recherche sur [Wikipédia](https://fr.wikipedia.org/wiki/Concours_Eurovision_de_la_chanson#Villes_h%C3%B4tes) :

![Eurovision](/assets/images/Shutlock-ctf_2024/Osint/Operation_Gear_Grinder-Signalement_2_12/Eurovision.png)

Nous trouvons l'Italie.

Nous cherchons ensuite le logo qui ressemble à celui d'Île-de-France Mobilités :

![France1](/assets/images/Shutlock-ctf_2024/Osint/Operation_Gear_Grinder-Signalement_2_12/France1.png)

Nous trouvons le site [IRBMS](https://www.irbms.com/).

![irbms](/assets/images/Shutlock-ctf_2024/Osint/Operation_Gear_Grinder-Signalement_2_12/irbms.png)

Résumons toutes les informations dont nous disposons : 

Nous cherchons un athlète italien de moins de 180 cm, né en 1965, banni pour les 35-40 prochaines années, et qui a été détecté à deux reprises lors de tests ! 

Une simple recherche Google nous permet de trouver le nom **Roberto Barbi**.

[Roberto Barbi](https://en.wikipedia.org/wiki/Roberto_Barbi)

![Roberto](/assets/images/Shutlock-ctf_2024/Osint/Operation_Gear_Grinder-Signalement_2_12/Roberto.png)

Nous avons presque trouvé le flag, il nous manque plus que la molécule. Ici, on nous parle de **EPO**, qui fait référence à l'[érythropoïétine](https://en.wikipedia.org/wiki/Erythropoietin).

𝄞 FLAG : `SHLK{Roberto_Barbi_érythropoïétine}` 𝄞