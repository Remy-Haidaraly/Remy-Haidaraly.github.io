---
title: Le tour de l'arène
categories: [leHACK_2023, Steganographie]
tags: [PDF]
image: '/assets/images/leHACK_2023/leHACK.jpg'
---

## 𝄞 Introduction

![Intro](/assets/images/leHACK_2023/steganography/Le%20tour_de_l'arene/intro.png)

## 𝄞 Solution

![PDF1](/assets/images/leHACK_2023/steganography/Le%20tour_de_l'arene/echiquier.png)

Pour résoudre ce défi de stéganographie, j'ai utilisé plusieurs outils pour analyser le **fichier PDF** fourni.

![PDF2](/assets/images/leHACK_2023/steganography/Le%20tour_de_l'arene/PDF_analyse.png)

J'ai décidé d'approfondir mon investigation en utilisant l'outil **"peepdf"**.

![PDF3](/assets/images/leHACK_2023/steganography/Le%20tour_de_l'arene/peepdf1.png)
![PDF4](/assets/images/leHACK_2023/steganography/Le%20tour_de_l'arene/peepdf_tree.png)

Je n'ai trouvé aucune information intéressante à partir de cette analyse. J'ai essayé plusieurs techniques, mais celle qui m'a permis de trouver le flag est d'extraire le *texte du PDF* avec l'outil **pdftotext**.



![PDF5](/assets/images/leHACK_2023/steganography/Le%20tour_de_l'arene/text.png)

Une fois le texte extrait, j'ai remarqué que les chaînes semblaient être encodées en **base64** et ensuite en **zlib**. J'ai utilisé l'outil en ligne Cyberchef pour décoder ces chaînes. [Cyberchef](https://gchq.github.io/CyberChef/) pour décoder ces chaînes.

![HINT1](/assets/images/leHACK_2023/steganography/Le%20tour_de_l'arene/hint1.png)
![HINT2](/assets/images/leHACK_2023/steganography/Le%20tour_de_l'arene/hint2.png)
![Flag](/assets/images/leHACK_2023/steganography/Le%20tour_de_l'arene/flag.png)

En appliquant le même processus de décodage à la troisième chaîne, j'ai obtenu le flag recherché.


Nous pourrions réalisé un simple script python 
```python
import base64
import zlib

flag =zlib.decompress(base64.b64decode("eJxzzs9LL0osKc1JLMnMzytWUFQIyUhVSMtJTFfILFawUijOTczJSS1S0CjJLy1ROLw8UaEgv7QIxNDT09MEAMRyFmM=")).decode('utf-8')
print(flag)
````
![Flag_Python](/assets/images/leHACK_2023/steganography/Le%20tour_de_l'arene/flag_python.png)

𝄞 FLAG : `leHACK{smaller (tout ça pour ça...)}` 𝄞










