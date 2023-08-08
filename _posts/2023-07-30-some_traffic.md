---
title: SOMME_TRAFFIC
categories: [Forensic_TFC_CTF_2023]
tags: []
image: '/assets/images/TFC_CTF_2023/main.jpg'
---

## 𝄞 Introduction

![Intro](/assets/images/TFC_CTF_2023/Forensics/SOME_TRAFFIC/intro.png)


## 𝄞 Objectif 

L'objectif de ce challenge consiste à découvrir le flag avec le fichier *pcap*.


## 𝄞 Solution

Nous commençons par une analyse rapide du fichier pcap.

![Analysis](/assets/images/TFC_CTF_2023/Forensics/SOME_TRAFFIC/analysis.png)

Cependant, nous ne trouvons rien d'intéressant. Pour creuser davantage, nous utilisons l'outil **Wireshark**.

![Http](/assets/images/TFC_CTF_2023/Forensics/SOME_TRAFFIC/http.png)

Nous remarquons des requêtes **HTTP** sur un formulaire de téléchargement. Avec **Wireshark**, nous pouvons extraire ces images, car elles sont transférées via le protocole **HTTP**. Pour ce faire, nous allons dans *Fichier > Exporter les objets > HTTP*.


![Upload](/assets/images/TFC_CTF_2023/Forensics/SOME_TRAFFIC/upload.png)

Nous parvenons à extraire trois images :

![Donwload](/assets/images/TFC_CTF_2023/Forensics/SOME_TRAFFIC/download.png)

![Download2](/assets/images/TFC_CTF_2023/Forensics/SOME_TRAFFIC/download2.png)

![Download3](/assets/images/TFC_CTF_2023/Forensics/SOME_TRAFFIC/download3.png)

En analysant chacune de ces images, nous ne trouvons rien d'intéressant. Cependant, la première image semble avoir quelque chose visuellement intrigant lorsqu'on zoome sur la partie des pixels.


![Zoom](/assets/images/TFC_CTF_2023/Forensics/SOME_TRAFFIC/zoom.png)

On distingue différentes nuances de vert sur les pixels. Tentons de récupérer leurs valeurs en utilisant Python.


```python
from PIL import Image

image_path = "download.png"
image = Image.open(image_path)

width, height = image.size

for y in range (height):
    R, G, B = image.getpixel((0,y))
    print(G)
```

![Ascii](/assets/images/TFC_CTF_2023/Forensics/SOME_TRAFFIC/ascii.png)

Les résultats semblent être des codes ASCII. En utilisant la fonction **chr()** de Python, nous pouvons obtenir directement la valeur ASCII correspondant aux numéros trouvés.



```python
from PIL import Image

image_path = "download.png"
image = Image.open(image_path)


width, height = image.size


for y in range (height):
    R, G, B = image.getpixel((0,y))
    print(chr(G), end="")
```

![Flag](/assets/images/TFC_CTF_2023/Forensics/SOME_TRAFFIC/flag.png)


𝄞 FLAG : `TFCCTF{H1dd3n_d4t4_1n_p1x3ls_i5n't_f4n_4nd_e4sy_to_f1nd!}` 𝄞 


