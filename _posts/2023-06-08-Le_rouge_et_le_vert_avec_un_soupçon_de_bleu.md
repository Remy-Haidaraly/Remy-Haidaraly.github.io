---
title: Le Rouge et le vert, avec un soupçon de bleu
categories: [404CTF_2023, Steganographie_404]
tags: [Steganographie]
---

## 𝄞 Introduction

![Intro](/assets/images/404CTF_2023/Steganographie/Le_rouge_et_le_vert_avec_un_soupçon_de_bleu/intro.png)

## 𝄞 Solution

Dans ce défi de stéganographie, l'objectif est de retrouver un message caché dans le texte fourni.

![Texte](/assets/images/404CTF_2023/Steganographie/Le_rouge_et_le_vert_avec_un_soupçon_de_bleu/texte.png)

En examinant le texte, j'ai remarqué la présence d'une **série de chiffres** accompagnés de **couleurs**. Cela a piqué ma curiosité et semblait être une piste intéressante à suivre.

J'ai rapidement compris que la suite de chiffres correspondait à des **valeurs ASCII**. J'ai donc essayé de décoder ces chiffres en utilisant un outil en ligne comme [Dcode - Ascii](https://www.dcode.fr/ascii-code).

`76 321021089710332 115116581089795118 95 1109599 108 114115125`

![Dcode](/assets/images/404CTF_2023/Steganographie/Le_rouge_et_le_vert_avec_un_soupçon_de_bleu/dcode.png)

Il y avait plusieurs façons de trouver le reste du flag :

`L flag st:la_v_n_clrs}`

### 𝄞𝄞 Première méthode 

On pouvait essayer de deviner la phrase manquante, et rapidement on trouve : Le flag est : `la_vie_en_couleurs`

### 𝄞𝄞 Deuxième méthode 
Personnellement, j'ai choisi de rechercher le texte présent dans le défi, qui est le poème *"Lettre du voyant"* **d'Arthur Rimbaud.** Étant donné qu'il y avait des références à des couleurs dans le texte, j'ai supposé qu'il pourrait cacher **les valeurs ASCII des lettres manquantes** dans le flag. J'ai donc cherché un lien entre les couleurs mentionnées et Arthur Rimbaud.

![Couleur](/assets/images/404CTF_2023/Steganographie/Le_rouge_et_le_vert_avec_un_soupçon_de_bleu/couleur.png)

**A** --> Noir  
**E** --> Blanc  
**I** --> Rouge  
**U** --> Vert  
**O** --> Bleu  

Voila quelque chose de très intéressant :

![Couleur_rimbaud](/assets/images/404CTF_2023/Steganographie/Le_rouge_et_le_vert_avec_un_soupçon_de_bleu/couleur_rimbaud.png)

Grâce à cela, j'ai pu facilement trouver les lettres manquantes en me référant à notre texte initial :

`L flag st:la_v(rouge)(blanc)_n_c(bleu)(vert)l(blanc)(vert)rs}`

J'ai simplement remplacé chaque couleur par la lettre correspondante.

𝄞 FLAG : `la_vie_en_couleurs}` 𝄞


## 𝄞 Conclusion
La résolution de ce défi de stéganographie a nécessité une analyse attentive du texte, en se concentrant sur les chiffres et les couleurs. En utilisant différentes méthodes, j'ai pu révéler le message caché et trouver le flag.   
*Bravo à l'auteur de ce challenge très innovant et bien pensé !*
  







