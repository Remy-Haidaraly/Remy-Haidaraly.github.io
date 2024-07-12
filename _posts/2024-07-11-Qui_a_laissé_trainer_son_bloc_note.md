---
title: Qui a laissé traîner son bloc-note ?
categories: [Shutlock-CTF_2024, Web_shutlock]
tags: [Web]
image: '/assets/images/Shutlock-ctf_2024/logo.jpg'
---

## 𝄞 Introduction

![Intro](/assets/images/Shutlock-ctf_2024/Web/Qui_a_laissé_trainer_son_bloc_note_/intro.png)

## 𝄞 Solution

Un lien qui nous est fourni, nous redirige sur un panneau de connexion !

![Web](/assets/images/Shutlock-ctf_2024/Web/Qui_a_laissé_trainer_son_bloc_note_/web.png)

La première chose à faire est de regarder le code source de l'application web.

![Code](/assets/images/Shutlock-ctf_2024/Web/Qui_a_laissé_trainer_son_bloc_note_/code.png)

Nous trouvons un commentaire assez intéressant : 
𝄞 `<!-- Clé à n'utiliser que pour développer : VerySecretKey--!>` 𝄞

Si nous essayons de nous connecter, nous obtenons une erreur.

![Jwt](/assets/images/Shutlock-ctf_2024/Web/Qui_a_laissé_trainer_son_bloc_note_/jwt.png)

Nous remarquons dans l'URL un paramètre **Token** qui prend comme valeur une chaîne commençant par **eyJ**, qui est un token JWT. Le commentaire précédent prend tout son sens ! Nous devons manipuler ce token pour accéder à la page en tant qu'**admin**.

𝄞 `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJyb2xlIjoiZ3Vlc3QiLCJpYXQiOjE3MTk2OTYzOTJ9.LT34KrsgUaXuxBNVETTJD_sDBbDX7rxzXuqC41M7VRY` 𝄞

Nous pouvons entrer ce token sur le site [jwt.io](https://jwt.io).

![Jwt2](/assets/images/Shutlock-ctf_2024/Web/Qui_a_laissé_trainer_son_bloc_note_/jwt2.png)

Nous voyons notre rôle, qui est **guest**, et nous pouvons mettre une clé pour signer notre token. Nous allons essayer de changer le rôle en **admin** et utiliser la clé trouvée dans le commentaire pour signer le token.

![Jwt3](/assets/images/Shutlock-ctf_2024/Web/Qui_a_laissé_trainer_son_bloc_note_/jwt3.png)

𝄞 `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJyb2xlIjoiYWRtaW4iLCJpYXQiOjE3MTk2OTYzOTJ9.-33dSDZdC6WU-w7wiS7xR0wtu7V83CVHkDnPDFyDix4` 𝄞

Nous allons maintenant modifier l'URL :
𝄞 `http://57.128.85.25:50007/admin?token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJyb2xlIjoiYWRtaW4iLCJpYXQiOjE3MTk2OTYzOTJ9.-33dSDZdC6WU-w7wiS7xR0wtu7V83CVHkDnPDFyDix4` 𝄞

et rafraîchir la page !

![Web2](/assets/images/Shutlock-ctf_2024/Web/Qui_a_laissé_trainer_son_bloc_note_/web2.png)

Nous avons réussi à nous authentifier comme **admin** et trouvé le flag !

𝄞 FLAG : `SHLK{N3_l1s_pa5_l3s_not3s}` 𝄞