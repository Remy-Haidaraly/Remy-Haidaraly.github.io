---
title: Le Loup et le renard
categories: [404CTF_2023, Web_404]
tags: [Web, cookie, redirection, authentification]
image: '/assets/images/404CTF_2023/404CTF.jpg'
---

## 𝄞 Introduction

![Intro](/assets/images/404CTF_2023/Web/Le_Loup_et_le_renard/intro.png)

## 𝄞 Solution

Ce défi consiste en une **série de petites failles web** afin de trouver le flag à la fin du parcours.


## 𝄞𝄞 Partie 1 Authentification

![Authentification](/assets/images/404CTF_2023/Web/Le_Loup_et_le_renard/auth.png)

Nous avons un **formulaire d'authentification** où nous pouvons essayer des combinaisons courantes telles que *{admin:admin}*, *{admin:password123}*...
Il suffit de regarder simplement le code source de la page pour y trouver les informations d'authentification.


![Authentification_log](/assets/images/404CTF_2023/Web/Le_Loup_et_le_renard/auth_log.png)

`{admin:h5cf8gf2s5q7d}`

## 𝄞𝄞 Partie 2 Cookies 

![Cookies](/assets/images/404CTF_2023/Web/Le_Loup_et_le_renard/cookies.png)

On regarde notre cookie de session 

![IsAdmin](/assets/images/404CTF_2023/Web/Le_Loup_et_le_renard/isAdmin.png)

On change la valeur par **True** et il suffit ensuite de rafraîchir la page.

## 𝄞𝄞 Partie 3 Redirect

![Redirect](/assets/images/404CTF_2023/Web/Le_Loup_et_le_renard/redirect.png)

On regarde le code source de la page 

![Redirect](/assets/images/404CTF_2023/Web/Le_Loup_et_le_renard/partie4.png)

Nous remarquons un appel GET vers  */fable/partie-4-flag-final*.
Cependant, lorsque nous essayons d'accéder à cette URL, la page s'affiche brièvement avant de revenir à la page précédente.

Ainsi, plusieurs solutions sont possibles, comme l'utilisation d'un proxy tel que **Burp Suite** pour intercepter la requête avant la redirection.
Personnellement, j'ai utilisé l'outil curl.

```bash
curl https://le-loup-et-le-renard.challenges.404ctf.fr/fable/partie-4-flag-final
```

![Flag](/assets/images/404CTF_2023/Web/Le_Loup_et_le_renard/flag.png)


𝄞 FLAG : `404CTF{N0_frOn1_3nD_auTh3nt1ficAti0n}` 𝄞


## 𝄞 Conclusion
Ce défi web "Le Loup et le renard" comportait plusieurs failles différentes, notamment une vulnérabilité d'authentification, une manipulation de cookies et une redirection. En exploitant ces failles, nous avons réussi à obtenir le flag final.












