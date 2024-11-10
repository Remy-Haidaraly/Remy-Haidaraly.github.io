---
title: Bypass The Authentification
categories: [Purple_Pill_2024, Web]
tags: [web]
image: '/assets/images/Purple_Pill_2024/logo.png'
---

# 𝄞 Introduction

![Intro](/assets/images/Purple_Pill_2024/Web/Bypass_the_authentification/intro.webp)

Ce challenge a pour objectif de contourner un système d’authentification en exploitant une **faille d'injection SQL**, afin de bypass l'authentification et de récupérer le flag.

## 𝄞 Solution

![Accueil](/assets/images/Purple_Pill_2024/Web/Bypass_the_authentification/ladding_page.webp)

La page d'accueil présente un site classique, organisé en plusieurs sections. La seule section accessible et pertinente pour notre objectif est **Connexion Sécurisée**, qui mène à un formulaire d'authentification.

![Connexion](/assets/images/Purple_Pill_2024/Web/Bypass_the_authentification/pannel_connexion.webp)

En entrant des identifiants quelconques, l'application retourne un message d'erreur indiquant que le nom d'utilisateur ou le mot de passe est incorrect. Puisque nous n'avons aucune information au préalable sur d’éventuels identifiants, nous choisissons de tester une injection SQL pour contourner l'authentification.

### 𝄞𝄞 UNION SQLI

En injectant une simple apostrophe (`'`) dans le champ **username**, l'application réagit différemment et retourne un code d’erreur 500.

![Error](/assets/images/Purple_Pill_2024/Web/Bypass_the_authentification/error.webp)

Lorsque nous essayons d'entrer le mot **OR**, l'application le bloque et affiche un message d'erreur **"Entrée non valide"**.

![Blacklist](/assets/images/Purple_Pill_2024/Web/Bypass_the_authentification/filtre.webp)

Cela suggère que l’application utilise une blacklist pour empêcher certaines entrées susceptibles de conduire à une injection SQL. Nous devons donc trouver une autre méthode pour contourner l'authentification sans utiliser le mot **OR**.

Pour ce faire, nous avons utilisé le payload suivant :

```bash
fxoverflow'UNION select 1,2,3--
``` 

Il est crucial de respecter le même nombre de colonnes dans la requête SELECT pour éviter un code d'erreur 500.

Ce payload réussit à contourner le formulaire d'authentification et nous connecte sous l'identité de l’utilisateur "2".

Avec cette injection, la requête finale ressemble à ceci :

```sql
SELECT * FROM users WHERE username = 'fxoverflow' UNION SELECT 1,2,3--' AND password = 'user_input';
```
Cette requête :  
Effectue la sélection habituelle sur le tableau users avec le username = **'fxoverflow'**, mais cette condition échoue car l'utilisateur n'existe pas.  
Le **UNION** permet de combiner cette première requête avec **SELECT 1,2,3**, qui est exécutée même si la condition initiale est fausse.
Grâce au **--**, la vérification du mot de passe est ignorée, ce qui fait que l'application retourne une réponse réussie basée sur les résultats du UNION SELECT.

![Flag](/assets/images/Purple_Pill_2024/Web/Bypass_the_authentification/flag.webp)


𝄞 FLAG : `PPC2024{4UwxK287znVNp8}` 𝄞
