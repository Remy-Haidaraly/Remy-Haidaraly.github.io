---
title: Where's Wally again ?
categories: [leHACK_2023, Steganographie_leHACK]
tags: [LSB, Steganographie]
image: '/assets/images/leHACK_2023/leHACK.jpg'
---

## 𝄞 Introduction

![Intro](/assets/images/leHACK_2023/steganography/Where's_Wally_Again/Intro.png)

## 𝄞 Solution

Pour résoudre ce défi de stéganographie, j'ai commencé par analyser l'image fournie en utilisant plusieurs outils.

![Analyse](/assets/images/leHACK_2023/steganography/Where's_Wally_Again/Analyse.png)

Il y a plusieurs chose à vérifier sur un fichier au format **.png** telles que les *chunks*, *les filtres de couleur*, ainsi que des techniques couramment utilisées comme le *LSB (Least Significant Bit)*. J'ai utilisé l'outil **"zsteg"** pour chercher un message caché en utilisant la technique du LSB. 

![Flag](/assets/images/leHACK_2023/steganography/Where's_Wally_Again/flag.png)

Finalement, j'ai réussi à trouver le flag caché dans l'image en utilisant cet outil. Dans une compétition où le temps est limité, j'ai voulu gagner du temps plutôt que de créer un script Python personnalisé. Cela explique pourquoi j'ai utilisé **"zsteg"** pour résoudre ce défi rapidement et efficacement.

𝄞 FLAG : `leHACK{Charlie is in Paris (without Emily)}` 𝄞 

## 𝄞 Conclusion
En conclusion, j'ai résolu le défi "Where's Wally again ?" en analysant l'image fournie et en utilisant l'outil "zsteg" pour trouver le flag caché en utilisant la technique du LSB.







