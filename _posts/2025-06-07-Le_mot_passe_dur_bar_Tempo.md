---
title: Le mot passe dur bar Tempo
categories: [m1ndbr34k_2025, Forensic_m1ndbr34k_2025]
tags: [Forensic]  
image: '/assets/images/m1ndbr34k/logo.png'
---

## 𝄞 Introduction

![Intro](/assets/images/m1ndbr34k_2025/Forensic/Le_mot_passe_dur_bar_Tempo/intro.png)

---

## 🗂Contenu du fichier ZIP

- Le dump de 20Go

## Solution :

Nous allons analyser ce dump à l’aide de l’outil **Autopsy**.

![Autospy](/assets/images/m1ndbr34k_2025/Forensic/Le_mot_passe_dur_bar_Tempo/autopsy.webp)

En explorant les fichiers, rien d’inhabituel n’apparaît, il s’agit d’un dump d’une machine Windows quasi vide.
Il convient donc de se focaliser sur le synopsis, qui fait référence à une messagerie violette.
iil s’agit en réalité de ...... **Microsoft Teams**.

Pour analyser les messages **Teams** présents dans ce dump, un module spécifique est disponible. Il suffit de le télécharger puis de l’installer.

Une fois l’installation terminée, nous pouvons utiliser ce module pour accéder à la conversation Teams recherchée.

[teams](https://github.com/lxndrblz/forensicsim/tree/main)

![module](/assets/images/m1ndbr34k_2025/Forensic/Le_mot_passe_dur_bar_Tempo/module.webp)

![message](/assets/images/m1ndbr34k_2025/Forensic/Le_mot_passe_dur_bar_Tempo/message.webp)

surprise :) 

![Teams1](/assets/images/m1ndbr34k_2025/Forensic/Le_mot_passe_dur_bar_Tempo/teams.webp)

 𝄞 FLAG : `MB{TEAMS-IS-FUN}`𝄞

 

