---
title: Filesystem Intruder
categories: [Purple_Pill_2024, Web]
tags: [web, SSTI]
image: '/assets/images/Purple_Pill_2024/logo.png'
---

# 𝄞 Introduction

![Intro](/assets/images/Purple_Pill_2024/Web/Filesystem_intruder/intro.webp)

Ce challenge consiste à compromettre le serveur avec le compte administrateur afin de récupérer le flag.

## 𝄞 Solution

![Accueil](/assets/images/Purple_Pill_2024/Web/Filesystem_intruder/menu.webp)

La page d’accueil propose une fonctionnalité supplémentaire lorsque nous sommes connectés en tant qu’administrateur :
- **Ajouter un utilisateur**

### 𝄞𝄞 Ajouter un utilisateur

Nous avons la possibilité d’ajouter un utilisateur dans l’application.

![add](/assets/images/Purple_Pill_2024/Web/Filesystem_intruder/ajout%20utilisateur.webp)

En ajoutant l’utilisateur **fxoverflow**, un message de confirmation s’affiche, validant la création de l’utilisateur.

![add2](/assets/images/Purple_Pill_2024/Web/Filesystem_intruder/output.webp)

Nous remarquons que le champ **"username"**, que nous contrôlons, est reflété dans la réponse du serveur. Si ce champ n’est pas correctement filtré, cela pourrait nous permettre d'exploiter une vulnérabilité pour compromettre le serveur.  
Ici, nous tentons une injection de type SSTI (Server-Side Template Injection).

![ssti](/assets/images/Purple_Pill_2024/Web/Filesystem_intruder/ssti.webp)  
![ssti2](/assets/images/Purple_Pill_2024/Web/Filesystem_intruder/ssti2.webp)

Le serveur nous renvoie **49**, confirmant ainsi la vulnérabilité SSTI.

### Payload

Pour exploiter cette faille, nous utilisons un payload qui nous permet d’exécuter des commandes système et de compromettre le serveur afin de rechercher le flag.

{% raw %}
```python
{{ self.__init__.__globals__.__builtins__.__import__('os').popen('id').read() }}
```
{% endraw %}


Ce payload nous donne la capacité d'exécuter des commandes système.

![Burp](/assets/images/Purple_Pill_2024/Web/Filesystem_intruder/burp.webp)

Nous procédons alors à une énumération des fichiers sur le serveur pour repérer des éléments intéressants.

![Burp2](/assets/images/Purple_Pill_2024/Web/Filesystem_intruder/enum.webp)
![Burp3](/assets/images/Purple_Pill_2024/Web/Filesystem_intruder/enum2.webp)

Nous trouvons un fichier intéressant **.flags..**

En lisant le contenu de ce fichier, nous obtenons le flag.

![flag](/assets/images/Purple_Pill_2024/Web/Filesystem_intruder/flag.webp)

𝄞 FLAG : `PPC2024{w8zpU47VNKx2n8}` 𝄞