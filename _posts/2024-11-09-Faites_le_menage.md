---
title: Faites le ménage
categories: [Purple_Pill_2024, OSINT]
tags: [OSINT]
image: '/assets/images/Purple_Pill_2024/logo.png'
---

# 𝄞 Introduction

![Intro](/assets/images/Purple_Pill_2024/Osint/Faites_le_menage/intro.webp)

Ce challenge a pour objectif de retrouver la société de ménage du client.

## 𝄞 Solution

Pour ce faire, nous avons exploré le site internet en profondeur et découvert un fichier **robots.txt**.

![Robots](/assets/images/Purple_Pill_2024/Osint/Faites_le_menage/robots.webp)

Ce fichier *robots.txt* révèle l'existence d'un service **FTP**.

![FTP](/assets/images/Purple_Pill_2024/Osint/Faites_le_menage/ftp.webp)

En accédant à ce lien, nous trouvons de nombreux documents, dont un intitulé **"contract_menage.pdf"**, qui retient particulièrement notre attention.

![Menage](/assets/images/Purple_Pill_2024/Osint/Faites_le_menage/contrat.webp)

En lisant ce document, nous découvrons le nom de la société de ménage.

𝄞 FLAG : `PPC2024{cocooning_eclatant}` 𝄞