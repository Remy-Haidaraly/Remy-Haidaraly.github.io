---
title: Les Félicitations
categories: [404CTF_2023, Steganographie]
tags: [Steganographie]
---

## 𝄞 Introduction

![Intro](/assets/images/404CTF_2023/Steganographie/Les_Felicitations/intro.png)

## 𝄞 Solution

Dans ce défi de **stéganographie**, l'objectif est de **retrouver un message caché dans le texte.** 
Après plusieurs jours de recherche intensive, je n'ai trouvé aucun indice sur la façon dont le message était dissimulé. Le morse que l'on voit sur l'image est une fause piste. 

### 𝄞𝄞 Première Solution 
Après plusieurs jours de recherche intensive, aucune indication sur la manière dont le message était dissimulé n'a été trouvée. Bien que le morse présent sur l'image semblait être une piste, il s'est avéré être une fausse piste.

j'ai commencé à explorer différentes techniques appliquées aux textes. C'est ainsi que j'ai découvert une méthode appelée **"acrostiche"**.

`Un acrostiche est une forme de poésie ou de jeu littéraire où les premières lettres de chaque vers ou chaque ligne, lues verticalement, forment un mot, une phrase ou un message spécifique.`

J'ai donc tenté d'appliquer la technique de **l'acrostiche** au texte, mais je n'ai rien trouvé d'intéressant. Cependant, j'ai envisagé la possibilité que le message soit dissimulé sous la forme d'un **acronyme**. Après de nombreux jours de recherche, j'ai finalement décidé de prendre **la première lettre du premier vers de chaque paragraphe**. Cela m'a donné le résultat **"TBJ"**. 

![Flag1](/assets/images/404CTF_2023/Steganographie/Les_Felicitations/flag1.png)

Mais que signifie **"TBJ"**? Tout simplement **"Très bien joué"** !
### 𝄞𝄞 Deuxième Solution 

Une autre approche pour trouver le message caché consiste à prendre, pour chaque paragraphe :

- la première lettre de la première phrase
- la deuxième lettre de la deuxième phrase
- la troisième lettre de la troisième phrase, et ainsi de suite.
etc

![Flag](/assets/images/404CTF_2023/Steganographie/Les_Felicitations/flag.png)


𝄞 FLAG : `404CTF{TrèsBienJoué}` 𝄞

## 𝄞 Conclusion  
En résolvant ce défi de stéganographie intitulé "Les Félicitations", j'ai pu découvrir deux méthodes pour trouver le message caché dans le texte. La première consistait à utiliser l'acrostiche en prenant la première lettre du premier vers de chaque paragraphe, tandis que la deuxième approche consistait à extraire des lettres spécifiques de chaque phrase dans chaque paragraphe. Ces méthodes démontrent l'importance de la créativité et de l'exploration de différentes techniques lors de la résolution de défis de stéganographie.















