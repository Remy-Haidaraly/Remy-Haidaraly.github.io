---
title: La Quête du sens [1/3]
categories: [404CTF_2023, OSINT_404]
tags: [OSINT]
---

## 𝄞 Introduction

![Intro](/assets/images/404CTF_2023/OSINT/La_Quete_du_sens_1/intro.png)


## 𝄞 Solution

L'objectif de ce challenge est de **retrouver le nom du texte dont est issue la chanson fournie dans l'énoncé.**

Le fichier **MP3** dure **16** secondes et nous n'entendons que du **piano** pendant cette période. Mon premier réflexe a été de consulter les **métadonnées** de l'audio dans l'espoir de trouver des informations sur l'auteur, mais malheureusement, cela n'a rien donné. J'ai également essayé d'utiliser **Shazam** pour identifier la musique, mais j'ai obtenu plusieurs résultats incorrects.

Après plusieurs jours de blocage, j'ai décidé d'explorer une piste un peu plus originale. Cette année, le thème du **404CTF édition 2023** porte sur **les grandes figures de la littérature française**. J'ai donc pensé qu'il faudrait chercher la musique dont le texte est tiré d'une grande figure de la littérature française dont le nom commence par **"Mar"**. Après quelques recherches, je suis tombé sur ce [site](https://actus.booknode.com/2016/03/08/journee-de-la-femme-ces-femmes-qui-ont-marque-la-litterature/) où j'ai trouvé une femme très intéressante : **Marceline Desbordes-Valmore**.

![Google](/assets/images/404CTF_2023/OSINT/La_Quete_du_sens_1/google.png)

Nous avons donc retrouvé la musique. Il ne reste plus qu'à chercher le texte utilisé dans la musique. Après quelques recherches supplémentaires, il s'avère qu'il s'agit de la **poésie** intitulée **"Les séparés"**.

𝄞 FLAG : `404CTF{les_separes}` 𝄞


## 𝄞 Conclusion
Ce défi d'OSINT nous a poussés à utiliser notre créativité et à explorer des pistes alternatives pour résoudre le problème. Cela démontre l'importance de penser de manière originale et de considérer différents angles d'approche lors de la résolution de problèmes d'OSINT. D'ailleurs c'est une musique qui rentre dans ma playlist il s'avère que j'ai bien aimé la [musique](https://youtu.be/t-qbh3az3Rk).
  







