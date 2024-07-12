---
title: Le Quêteur Démasqué
categories: [Shutlock-CTF_2024, Osint_shutlock]
tags: [Osint]
image: '/assets/images/Shutlock-ctf_2024/logo.jpg'
---

## 𝄞 Introduction

![Intro](/assets/images/Shutlock-ctf_2024/Osint/Le_Queteur_demasqué/intro.png)

## 𝄞 Solution

Un fichier **.txt** nous est fourni contenant une adresse de cryptomonnaie.

𝄞 Adresse cryptomonnaie : `bc1q3gys9pv79uxvnqau32m72ztcp48r30vuc0lqz3` 𝄞

La première chose que j'ai essayée est d'en savoir plus sur cette adresse via différents sites d'analyse d'adresses de cryptomonnaie comme [blockchain.com](https://www.blockchain.com/explorer/addresses/btc/bc1q3gys9pv79uxvnqau32m72ztcp48r30vuc0lqz3).

![info](/assets/images/Shutlock-ctf_2024/Osint/Le_Queteur_demasqué/info.png)

Malheureusement, nous ne trouvons rien de spécial. À partir de là, j'étais bloqué un bon moment... jusqu'à ce que je relise bien les images d'introduction du challenge !

![Clue](/assets/images/Shutlock-ctf_2024/Osint/Le_Queteur_demasqué/clue.png)

On cherche un endroit qui parle de dons pour le Listenbourg pour les Jeux Olympiques. Je cherche sur plusieurs réseaux jusqu'à tomber sur une discussion [telegram.com](https://web.telegram.org/a/#-1002042882160) très intéressante !

![1](/assets/images/Shutlock-ctf_2024/Osint/Le_Queteur_demasqué/1.png)

On peut voir que le message est écrit par un certain **@CrypThomas_LIS**. Je vais donc commencer à chercher ce **pseudo** sur différents réseaux ! On trouve un profil intéressant sur [x.com](https://x.com/CrypThomas_LIS).

![Tweet](/assets/images/Shutlock-ctf_2024/Osint/Le_Queteur_demasqué/tweet.png)

On tombe sur ce tweet où Thomas semble se plaindre d'une personne qui l'identifie comme arnaqueur. Le problème c'est que si nous cliquons sur ce lien dont il fait référence dans le tweet, on s'aperçoit que le tweet est supprimé ! [x.com](https://x.com/crypto_report_x/status/1795199566364528954).

![404](/assets/images/Shutlock-ctf_2024/Osint/Le_Queteur_demasqué/404.png)

Nous devons donc trouver un moyen de retrouver le contenu de ce tweet. Pour cela, nous pouvons utiliser par exemple [WayBackMachine](https://web.archive.org/). Le problème, c'est que **WayBackMachine** gère mal les snapshots sur **X.com**, alors nous allons trouver une autre alternative. Je vais utiliser un site comme **WayBackMachine**, mais qui ne pose pas de problème sur **X.com**.

[Archive.ph](https://archive.ph/) j'utilise ce site avec le lien du tweet effacé et nous trouvons une archive !!

![Found](/assets/images/Shutlock-ctf_2024/Osint/Le_Queteur_demasqué/found.png)

Nous avons plusieurs informations dont l'adresse **thomaskb94270@gmail.com**.

Maintenant, nous devons trouver un maximum de choses sur cette adresse. Pour ce faire, je vais utiliser le site [Epios.com](https://epieos.com/?q=thomaskb94270%40gmail.com&t=email) avec l'adresse **thomaskb94270@gmail.com**.

![Found2](/assets/images/Shutlock-ctf_2024/Osint/Le_Queteur_demasqué/found2.png)

Nous avons trouver plusieurs choses intéressantes, dont l'accès public à son [Google Calendar](https://calendar.google.com/calendar/u/0/embed?src=thomaskb94270@gmail.com&pli=1).

On remarque qu'il y a un rendez-vous mensuel *le samedi 27 juillet 2024*. Si on clique dessus, nous pouvons retrouver le flag !

![Flag](/assets/images/Shutlock-ctf_2024/Osint/Le_Queteur_demasqué/flag.png)

𝄞 FLAG : `SHLK{42_Avenue_Listen_1er_75003_Paris_France}` 𝄞