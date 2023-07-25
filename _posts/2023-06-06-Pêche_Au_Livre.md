---
title: Pêche au livre
categories: [404CTF_2023, Forensic_404]
tags: [Wireshark]
---

## 𝄞 Introduction
![Intro](/assets/images/404CTF_2023/Forensic/Peche_au_livre/intro.png)


Nous avons un fichier **pcapng** à analyser.

## 𝄞 Solution

![Capture](/assets/images/404CTF_2023/Forensic/Peche_au_livre/capture.png)
En ouvrant le **fichier pcap avec Wireshark**, nous remarquons que trois protocoles ont été utilisés lors de la communication : **HTTP, ICMPv6 et TCP.**

En examinant rapidement les paquets HTTP, nous constatons des requêtes **GET** vers des images. Étant donné qu'il s'agit du protocole **HTTP**, nous pouvons récupérer ces images en utilisant la fonctionnalité **d'exportation** de Wireshark. Pour cela, nous allons dans le menu **"File"**, puis **"Export Objects"**, et enfin **"HTTP"**. Nous choisissons l'option **"Save All"** pour enregistrer toutes les images.

Après avoir exporté les images, nous obtenons trois images. En les examinant, nous trouvons le flag caché dans l'une d'entre elles.
![Images](/assets/images/404CTF_2023/Forensic/Peche_au_livre/images.png) 


𝄞 FLAG : `404CTF{345Y_W1r35h4rK}` 𝄞

## 𝄞 Conclusion
Pour résoudre ce challenge, nous avons utilisé Wireshark pour analyser les données de communication, identifié les requêtes HTTP contenant des images et exporté ces images pour les examiner et trouver le flag.
