---
title: En Profondeur
categories: [404CTF_2023, Steganographie_404]
tags: [Steganographie]
---

## 𝄞 Introduction

![Intro](/assets/images/404CTF_2023/Steganographie/En_Profondeur/intro.png)

## 𝄞 Solution


Dans ce défi de stéganographie, l'objectif est de **retrouver un message caché dans le texte fourni.** 

![Texte](/assets/images/404CTF_2023/Steganographie/En_Profondeur/texte.png)

Le texte initial ne révèle rien de suspect, mais une analyse plus approfondie révèle des différences de **nombre d'espaces entre certains mots**. J'ai noté les mots qui présentent ces différences : **[Paris, Marseille, Allemagne, Finlande, 10, 15, 34, 6, voiture, avion]**. Bien que cela soit prometteur, cela ne donne aucune indication claire pour le moment.

Pendant mes recherches pour le défi précédent, **"Les Félicitations"**, j'ai découvert cette [page](https://en.wikipedia.org/wiki/ASCII_stereogram) sur les **stéréogrammes**. 

`Les stéréogrammes sont des images en deux dimensions qui, lorsqu'elles sont observées d'une certaine manière, créent une illusion de profondeur et donnent une impression tridimensionnelle à l'image. Cette technique utilise deux images légèrement différentes superposées, chaque image étant vue séparément par chaque œil. Lorsque les deux images sont combinées par le cerveau, un effet de **profondeur** est créé, donnant l'impression que l'image est en relief.`

Sur cette même page, je tombe sur un texte similaire.
![Indice](/assets/images/404CTF_2023/Steganographie/En_Profondeur/indice.png)

J'ai utilisé un outil appelé **"stegsolve"** qui permet de faire de nombreuse manipulation sur des images, il propose notament une fonction **Stereogram Solver** pour superposer les deux textes. Voici le résultat obtenu :
![Flag](/assets/images/404CTF_2023/Steganographie/En_Profondeur/flag.png)

Une autre méthode consiste à utiliser l'outil **"Paint"** pour superposer les deux textes et avoir un meilleure rendu :

![Paint](/assets/images/404CTF_2023/Steganographie/En_Profondeur/paint.png)

Il est un peu difficile de lire le texte, mais en se référant au texte original, on peut déduire ce qui est écrit. On retrouve une liste similaire à celle que j'avais trouvée lors de ma première analyse : **[Paris, Marseille, Allemagne, Finlande, 10, 15, 66, Versailles, avions].**

En lisant attentivement le texte du défi, on découvre que **M. Valmont** n'a pas son permis. J'ai donc décalé le texte en superposant les mots **"Avions"** :

![Flag2](/assets/images/404CTF_2023/Steganographie/En_Profondeur/flag2.png)

Maintenant, on peut voir les mots **[Paris, Finlande, 15, 6, Avions].**

𝄞 FLAG : `404CTF{paris_finlande_15_6_avions}` 𝄞

## 𝄞 Conclusion
Ce défi de stéganographie était plus complexe que prévu, nécessitant une analyse approfondie du texte fourni. En utilisant la technique des **stéréogrammes** et en superposant les deux textes, j'ai pu révéler le message caché.