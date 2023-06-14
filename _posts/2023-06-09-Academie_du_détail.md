---
title: L'Académie du détail
categories: [404CTF_2023, Web]
tags: [JWT,Web]
---

## 𝄞 Introduction

![Intro](/assets/images/404CTF_2023/Web/Academie_du_détail/intro.png)

## 𝄞 Solution
L'objectif du challenge consiste à se connecter en tant qu'**admin** pour accéder à l'onglet **Liste des membres**.
![Connexion](/assets/images/404CTF_2023/Web/Academie_du_détail/Connexion.png)


![Authentification](/assets/images/404CTF_2023/Web/Academie_du_détail/login.png)

Le challenge présente un formulaire **d'authentification** où l'utilisateur doit entrer un nom d'utilisateur et un mot de passe pour se connecter. Si nous entrons des valeurs aléatoires dans ces champs, la page d'accueil affiche **un nouvel onglet** et génère un **jeton JWT** *(JSON Web Token)*.

![JWT](/assets/images/404CTF_2023/Web/Academie_du_détail/jwt.png)

En tentant d'accéder à l'onglet **"Liste des membres"** nous obtenons l'erreur suivante : 
![Erreur](/assets/images/404CTF_2023/Web/Academie_du_détail/erreur.png)

En tentant de se connecter avec le nom d'utilisateur **"admin"**, un message d'erreur s'affiche, ce qui suggère qu'un compte **admin existe**.
![Admin](/assets/images/404CTF_2023/Web/Academie_du_détail/admin.png)

## 𝄞𝄞 Partie 2 JWT

Au départ, j'ai envisagé une possible **faille SQL** pour me connecter en tant **qu'administrateur**, mais cela n'a rien donné. J'ai donc décidé de me concentrer sur l'analyse du **jeton JWT** généré avec un compte aléatoire.

Il est possible de **déchiffrer** le **JWT** en utilisant l'outil [jwt.io](https://jwt.io/)
![JWTIO](/assets/images/404CTF_2023/Web/Academie_du_détail/jwtio.png)

Il existe différentes technique d'exploitation sur les tokens JWT. 

J'ai remplacé **l'algorithme** par la valeur **"none"** et modifié le **"username"** en le remplaçant par **"admin"**. Cela m'a permis d'obtenir un nouveau JWT : 
`eyJhbGciOiJub25lIiwidHlwIjoiSldUIn0.eyJ1c2VybmFtZSI6ImFkbWluIiwiZXhwIjoxNjg2MzcxMjA2fQ.6JUuOqW00Y_2pUoRAooEkVDfWoWSjsm8U2e11UV1qjk.`

`Attention à ne pas oublier un . à la fin du JWT afin d'avoir une signature "vide"`

En utilisant ce nouveau **JWT**, j'ai pu accéder à l'onglet **"Liste des membres"** qui était réservé à l'administrateur.

![Flag](/assets/images/404CTF_2023/Web/Academie_du_détail/flag.png)


𝄞 FLAG : `404CTF{JWT_M41_1MP13M3N73_=L35_Pr0813M35}` 𝄞


## 𝄞 Conclusion
En résolvant le défi "L'Académie du détail", j'ai réussi à trouver une solution en exploitant le JWT généré par le formulaire d'authentification. En remplaçant les valeurs de l'algorithme et du nom d'utilisateur dans le JWT, j'ai pu me connecter en tant qu'administrateur et accéder à l'onglet "Liste des membres". Ce défi met en évidence l'importance de comprendre le fonctionnement des jetons JWT et les possibles failles de sécurité qui peuvent en découler.















