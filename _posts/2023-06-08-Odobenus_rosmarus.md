---
title: Odobenus Rosmarus
categories: [404CTF_2023, Steganographie]
tags: [Morse]
---

## 𝄞 Introduction

![Intro](/assets/images/404CTF_2023/Steganographie/Odobenus_rosmarus/intro.png)

## 𝄞 Solution

Dans ce défi de stéganographie, l'objectif est de **retrouver un message caché dans le texte fourni.** 
En examinant attentivement le texte, j'ai remarqué que certaines lettres étaient mises en évidence : **[C,L,E].**
Cependant, cela ne semblait pas fournir de message clair pour le moment. J'ai décidé de faire une recherche rapide sur Internet du titre du challenge et j'ai découvert que **"Odobenus Rosmarus"** est une espèce de morse, ce qui constitue un indice important.

![Morse](/assets/images/404CTF_2023/Steganographie/Odobenus_rosmarus/morse.png)

Le **morse** est un système de communication utilisant des **bips courts** (représentés par des points) et des **bips longs** (représentés par des tirets). Les espaces entre les bips et les mots sont également importants. En utilisant les indications du titre et du texte, j'ai associé les lettres **C, L et E** aux signaux du morse de la manière suivante :

𝄞 Chaine : `CCLCECLELCLCECCECLCCECECLCCECELLELLLECLCECCCEC}` 𝄞

- **C** correspond à un bip court
- **L** correspond à un bip long 
- **E** correspond à un espace

Ainsi on n'a le code morse suivant : 

𝄞 Morse : `..-. .- -.-. .. .-.. . .-.. . -- --- .-. ... .}` 𝄞

Je décode le morse avec [Dcode - Morse](https://www.dcode.fr/morse-code).

![Flag](/assets/images/404CTF_2023/Steganographie/Odobenus_rosmarus/flag.png)

𝄞 FLAG : `404CTF{FACILELEMORSE}` 𝄞


## 𝄞 Conclusion
En résolvant ce défi, j'ai réussi à décoder le message Morse caché dans le texte en utilisant les indices présents dans le titre et le contenu.
  







