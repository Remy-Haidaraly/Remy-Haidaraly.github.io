---
title: Operation Gear Grinder - Signalement 0/12
categories: [Shutlock-CTF_2024, Osint_shutlock]
tags: [Osint]
image: '/assets/images/Shutlock-ctf_2024/logo.jpg'
---

## 𝄞 Introduction

![Intro](/assets/images/Shutlock-ctf_2024/Osint/Operation_Gear_Grinder-Signalement_0_12/intro.png)

## 𝄞 Solution

Nous avons à notre disposition un fichier **.eml**.

> L’extension de fichier **.eml** fait référence à des fichiers texte simples dans lesquels un email complet, comprenant toutes les pièces jointes, peut être stocké sous forme de texte.
{: .prompt-info }

Nous pouvons ouvrir ce fichier **.eml** avec n'importe quel éditeur, comme Notepad, Sublime Text, etc.

Lorsque nous ouvrons ce fichier **.eml**, nous pouvons lire le contenu du mail et nous trouvons également une grande chaîne en base64 que nous allons pouvoir décoder.

![eml1](/assets/images/Shutlock-ctf_2024/Osint/Operation_Gear_Grinder-Signalement_0_12/eml1.png)

![eml2](/assets/images/Shutlock-ctf_2024/Osint/Operation_Gear_Grinder-Signalement_0_12/eml2.png)

Nous décodons la chaîne en base64 sur le site [CyberChef](https://gchq.github.io/CyberChef/).

## 𝄞 Decode

![decode](/assets/images/Shutlock-ctf_2024/Osint/Operation_Gear_Grinder-Signalement_0_12/decode.png)

Voici l'image entière obtenue :

![final](/assets/images/Shutlock-ctf_2024/Osint/Operation_Gear_Grinder-Signalement_0_12/final.png)

Sur le côté gauche de la feuille, nous pouvons retrouver un prénom et un nom : **Christophe Durandier**.

𝄞 FLAG : `SHLK{Christophe_Durandier}` 𝄞