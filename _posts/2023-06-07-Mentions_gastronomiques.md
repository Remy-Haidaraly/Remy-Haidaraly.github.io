---
title: Mentions gastronomiques
categories: [404CTF_2023, OSINT]
tags: [OSINT]
---

## 𝄞 Introduction

![Intro](/assets/images/404CTF_2023/OSINT/Mentions_gastronomiques/intro.png)


## 𝄞 Solution

L'objectif de ce challenge est de trouver le nom du restaurant et le prix qu’elle y a payé.

La seule information interéssante que nous disposons est le nom **"Margot Paquet"**
Après plusieurs recherche sur internet nous trouvons un compte [Instagram Margot Paquet](https://www.instagram.com/margot.paquet/)
 
![Insta](/assets/images/404CTF_2023/OSINT/Mentions_gastronomiques/insta.png)

Ce compte semble prometteur. Après avoir examiné chaque photo et description détaillée du profil, nous avons trouvé des informations intéressantes, mais rien concernant **la localisation du restaurant**. Cependant, nous avons remarqué que **Margot Paquet** a été **"taguée"** par le compte **futurionix** [Instagram Futurionix](https://www.instagram.com/futurionix/) sur deux photos.

L'une des deux photos est très interrésante. 
![Royal](/assets/images/404CTF_2023/OSINT/Mentions_gastronomiques/royal.png)

Nous pouvons en déduire que **Margot Paquet** était présente lors de ce *déjeuner d'affaires le **26 avril***. La photo montre la vue visible au moment de leur départ. Une simple recherche inversée sur cette image nous permet de trouver le nom de l'endroit que nous voyons, il s'agit du **Pont Royal**.

![Reverse](/assets/images/404CTF_2023/OSINT/Mentions_gastronomiques/reverse.png)


Avant de commencer à chercher le restaurant, nous pouvons déjà découvrir ce que **Margot Paquet** a mangé le **26 avril**.

![Plats](/assets/images/404CTF_2023/OSINT/Mentions_gastronomiques/plats.jpg)

Il est peu probable que Margot ait mangé deux plats différents. En se basant sur le commentaire concernant **le boeuf bourguignon**, nous pouvons déduire qu'elle a commandé ce plat ainsi qu'une **tarte tatin**.

### 𝄞𝄞 Google Maps
Avec toutes ces informations, nous cherchons un restaurant près du **Pont Royal** qui propose une **tarte tatin** et du **boeuf bourguignon à moins de 15€**.

![Restaurant](/assets/images/404CTF_2023/OSINT/Mentions_gastronomiques/restaurant.png)
Nous constatons qu'il y a plusieurs restaurants à proximité. Après plusieurs recherches, nous avons découvert que seul le restaurant **La Frégate** propose une **tarte tatin** et un **boeuf bourguignon à moins de 15€** dans son menu.

![Cartes](/assets/images/404CTF_2023/OSINT/Mentions_gastronomiques/carte.png)
Ne sachant pas quelle **tarte tatin** est la bonne, j'ai essayé avec les deux tartes, et il s'est avéré que c'était celle à 9€.

𝄞 FLAG : `404CTF{la_fregate_22.5}` 𝄞

## 𝄞 Conclusion
En utilisant des techniques **d'OSINT**, nous avons réussi à retrouver le nom du **restaurant** visité par **Margot Paquet** et le **prix** qu'elle a payé pour son repas. Cette enquête a mis en évidence l'importance de l'examen attentif des informations disponibles en ligne, des images, des tags et des commentaires pour obtenir des indices précieux. En combinant ces indices, nous avons pu localiser le restaurant et identifier le plat spécifique qu'elle a commandé. L'OSINT s'avère être un outil puissant pour résoudre des défis comme celui-ci et pour obtenir des informations utiles à partir de sources ouvertes.
