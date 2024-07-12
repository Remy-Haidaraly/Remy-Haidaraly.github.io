---
title: Il était une fois un samurai
categories: [Shutlock-CTF_2024, Misc_shutlock]
tags: [Misc]
image: '/assets/images/Shutlock-ctf_2024/logo.jpg'
---

## 𝄞 Introduction

![Intro](/assets/images/Shutlock-ctf_2024/Misc/Il_etait_une_fois_un_samurai/intro.png)

## 𝄞 Solution

Dans l'image de l'introduction, on nous parle d'une énigme se trouvant là où on a fait une croix sur l'oiseau bleu. On mentionne également **LeSamuraiSilencieux** et le cinéma franco-italien des temps modernes.

La phrase : 𝄞 `croix sur l'oiseau bleu` 𝄞 fait clairement référence à Twitter devenu [X.com](https://x.com).

Nous allons donc chercher le compte **LeSamuraiSilencieux** sur **X.com** et nous trouvons un profil intéressant [X.com](https://x.com/samuraislcx).

![X](/assets/images/Shutlock-ctf_2024/Misc/Il_etait_une_fois_un_samurai/x.png)

En cherchant ailleurs que sur [X.com](https://x.com), nous trouvons également **LeSamuraiSilencieux** sur [Github](https://github.com). Voici son [Github](https://github.com/LeSamuraiSilencieux/).

![Github](/assets/images/Shutlock-ctf_2024/Misc/Il_etait_une_fois_un_samurai/github.png)

Nous trouvons un repository intéressant du nom de "**ToPost**".

![X2](/assets/images/Shutlock-ctf_2024/Misc/Il_etait_une_fois_un_samurai/x2.png)

Nous retrouvons un texte qui nous parle d'hashtags dans le dernier post du *12/05* et un mot de passe **#CinemaJP2024!**.

![X3](/assets/images/Shutlock-ctf_2024/Misc/Il_etait_une_fois_un_samurai/x3.png)

Il est mentionné une technique de stéganographie. Le texte et les hashtags font référence à un outil de stéganographie utilisé pour cacher des données dans une image. Cet outil est **[stegide](https://steghide.sourceforge.net/)**.

Nous pouvons donc utiliser la commande suivante : 

```bash
steghide extract -sf final.jpg
```
Avec comme mot de passe : **CinemaJP2024!**

Ce qui nous donne un fichier **.txt** avec le flag dedans ! 

𝄞 FLAG : `SHLK{Gé5a5d_M0ul1n}!` 𝄞