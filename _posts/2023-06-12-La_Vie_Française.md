---
title: La Vie Française
categories: [404CTF_2023, Web]
tags: [cookie, UNION_SQLI, Web]
---

## 𝄞 Introduction

![Intro](/assets/images/404CTF_2023/Web/La_vie_française/intro.png)
L'objectif de ce challenge est d'utiliser **une faille d'injection SQL UNION** pour se connecter en tant **qu'administrateur**.

## 𝄞 Solution
![Accueil](/assets/images/404CTF_2023/Web/La_vie_française/accueil.png)

La page d'accueil nous présente un lien pour **se connecter** et un lien pour **postuler** qui nous permet de nous **enregistrer**.
La première approche consiste à essayer une **faille SQL** sur le formulaire d'authentification pour se connecter en tant qu'administrateur.

![Sqli_no](/assets/images/404CTF_2023/Web/La_vie_française/sqli_no.png)

Cependant, nous sommes rapidement confrontés à une limitation : **le formulaire n'accepte que les caractères alphanumériques**, excluant ainsi l'utilisation de *guillemets*, de *parenthèses* ou d'autres caractères spéciaux.

Le compte administrateur **"admin"** a été désactivé, donc nous devons trouver une autre méthode pour exploiter la faille SQL et trouver un compte administrateur.

![Admin](/assets/images/404CTF_2023/Web/La_vie_française/admin.png)

La seule option qui reste est de créer un compte en utilisant le lien de **"postuler"**. Nous allons créer un compte avec le nom d'utilisateur et le mot de passe **"toto"**.

![Toto](/assets/images/404CTF_2023/Web/La_vie_française/toto.png)

Une fois connecté, si nous essayons d'accéder à la page **"/admin"**, nous obtenons une erreur indiquant que nous ne sommes pas autorisés à y accéder.
![Erreur_Admin](/assets/images/404CTF_2023/Web/La_vie_française/erreur_admin.png)

Les seuls éléments manipulables par l'utilisateur sont :

- Le formulaire d'authentification (qui n'est pas exploitable comme nous l'avons vu précédemment).
- Le cookie de session UUID.

### 𝄞𝄞 UNION SQLI 

Nous allons essayer de faire une injection SQL sur le **cookie de session**. Si nous utilisons une valeur aléatoire, nous sommes redirigés vers "/login".
![Test](/assets/images/404CTF_2023/Web/La_vie_française/test.png)

Essayons maintenant de faire une injection SQL !

![Sqli1](/assets/images/404CTF_2023/Web/La_vie_française/sqli1.png)
En utilisant le payload :
`' OR 1=1-- -`
Nous constatons que nous avons une faille SQL dans le cookie de session. Nous allons maintenant essayer de déterminer combien de **colonnes peuvent être exploitées** et si elles **s'affichent ou non dans la construction de la page.**

![Sqli2](/assets/images/404CTF_2023/Web/La_vie_française/sqli2.png)
En utilisant le payload :
`' UNION SELECT 1,2,3-- -`
Nous constatons que **trois colonnes** sont exploitables et seulement **deux** sont affichées dans la construction de la page.

Nous allons maintenant déterminer la base de données sur laquelle nous nous trouvons en utilisant la fonction **database()**.

![Sqli3](/assets/images/404CTF_2023/Web/La_vie_française/sqli3.png)
En utilisant le payload :
`' UNION SELECT database(),2,3-- -`
Nous découvrons que nous sommes actuellement sur la base de données **"usersdb"**.


Nous allons ensuite essayer de déterminer **les tables disponibles dans cette base de données** 
![Sqli4](/assets/images/404CTF_2023/Web/La_vie_française/sqli4.png)
en utilisant le payload :
`' UNION SELECT TABLE_NAME,TABLE_SCHEMA,3 from INFORMATION_SCHEMA.TABLES where table_schema='usersdb'-- -`
Nous découvrons qu'il y a une table appelée **"users"** dans la base de données **"usersdb"**.

Nous allons maintenant déterminer **les noms des colonnes dans la table "users"**
![Sqli5_false](/assets/images/404CTF_2023/Web/La_vie_française/sqli5_false.png)
En utilisant le payload :
`' UNION select COLUMN_NAME,TABLE_SCHEMA,3 from INFORMATION_SCHEMA.COLUMNS where table_name='users'-- -`
Nous ne trouvons qu'une seule colonne, qui est **"id"**. Nous devons utiliser la fonction **"group_concat"** pour concaténer les valeurs en une seule chaîne, séparée par une virgule et voir toutes les colonnes ! .

![Sqli5](/assets/images/404CTF_2023/Web/La_vie_française/sqli5.png)
En utilisant le payload :
`' UNION select GROUP_CONCAT(COLUMN_NAME),TABLE_SCHEMA,3 from INFORMATION_SCHEMA.COLUMNS where table_name='users'-- -`
Nous obtenons toutes les colonnes de la tables **users**.

Les colonnes qui nous intéressent sont : **"id", "username", "password" et "status".**

Nous allons maintenant regarder le contenu de la table **"users"** en utilisant les colonnes mentionnées précédemment
![Sqli6](/assets/images/404CTF_2023/Web/La_vie_française/sqli6.png)
En utilisant le payload :
`'UNION SELECT group_concat(id,'|', username,'|',password,'|', status SEPARATOR '\n'),NULL,3 FROM users-- -`
Nous pouvons voir qu'il y a un seul compte **"admin"** avec les informations suivantes : *{madeleineforestier:fo2DVkgShz2pPJ}*.

#### 𝄞𝄞 Authentification en tant qu'administrateur

Maintenant, nous avons **deux options** pour nous connecter en tant qu'**administrateur** :

- Récupérer l'**UUID** avec la SQLI pour l'utilisateur "madeleineforestier" et le remplacer.
- Se connecter en utilisant les identifiants de l'administrateur.

Une fois connecté en tant qu'**administrateur**, nous accédons à la page **"/admin"** pour obtenir le flag !

![Flag](/assets/images/404CTF_2023/Web/La_vie_française/flag.png)

𝄞 FLAG : `404CTF{B3w4Re_th3_d3STruct1v3s_Qu0tes}` 𝄞


## 𝄞 Conclusion
En utilisant une faille d'injection SQL UNION sur le cookie de session, nous avons pu contourner les limitations du formulaire d'authentification et accéder au compte administrateur.



















