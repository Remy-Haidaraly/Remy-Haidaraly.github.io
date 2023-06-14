---
title: L'Épistolaire moderne
categories: [404CTF_2023, Web]
tags: [JWT, Web]
---

## 𝄞 Introduction

![Intro](/assets/images/404CTF_2023/Web/epistolaire_moderne/intro.png)


## 𝄞 Solution
L'objectif du challenge est trouver un moyen de se connecter en tant qu'administrateur.

![Accueil](/assets/images/404CTF_2023/Web/epistolaire_moderne/accueil.png)
Sur la page d'accueil, nous avons la possibilité de nous inscrire ou de nous connecter en utilisant un lien.

En examinant la page d'**authentification**, Nous pouvons essayer une **injection SQL** mais cela n'est visiblement pas possible. La seule option qui nous reste est de créer un compte en tant qu'invité.

![Auth](/assets/images/404CTF_2023/Web/epistolaire_moderne/authentification.png)

Une fois le compte créé, nous pouvons engager une conversation avec un "bot" appelé **Princesse de Clèves**.
Bien que le mot *"flag"* ne nous permette pas d'obtenir le bon flag, nous remarquons la présence d'un cookie **JWT**.
![Chat](/assets/images/404CTF_2023/Web/epistolaire_moderne/chat.png)
Nous décidons donc de le déchiffrer à l'aide de [jwt.io](https://jwt.io/).
![Jwt](/assets/images/404CTF_2023/Web/epistolaire_moderne/jwt.png)





Nous constatons qu'il n'y a pas de champ qui renseigne notre nom d'**utilisateur**, mais plutôt un champ **public_id**. Il va donc être difficile de manipuler et d'exploiter ce token pour en tirer quelque chose.

Après plusieurs tentatives pour trouver un moyen d'obtenir un compte administrateur, je décide d'envoyer une URL à **Princesse de Clèves** pour voir ce qui se passe.

![Jwt2](/assets/images/404CTF_2023/Web/epistolaire_moderne/jwt2.png)
C'est très intéressant, car nous obtenons un nouveau JWT. J'ai d'abord cru qu'il s'agissait de mon propre token, alors j'ai essayé de le déchiffrer en utilisant le même site mentionné précédemment.

![Jwt3](/assets/images/404CTF_2023/Web/epistolaire_moderne/jwt3.png)
Nous constatons que la valeur du **champ public_id** est différente. Je décide donc d'utiliser ce nouveau cookie pour me connecter.

![Flag](/assets/images/404CTF_2023/Web/epistolaire_moderne/flag.png)
Nous découvrons un nouvel onglet intitulé **"Notes personnelles"** où se trouve le flag !

𝄞 FLAG : `404CTF{L34k_d3_C00k13s_s3cr3ts}` 𝄞


## 𝄞 Conclusion
En conclusion, le défi de l'épistolaire moderne nous a placés face à une situation où l'injection SQL n'était pas possible, nous obligeant à explorer d'autres méthodes pour avancer. C'est ainsi que nous avons réussi à récupérer le cookie de l'administrateur en interagissant avec le bot. Ce défi souligne l'importance de faire preuve de réflexion créative et d'explorer différentes approches pour résoudre les problèmes de sécurité.























