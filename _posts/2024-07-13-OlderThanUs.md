---
title: OlderThanUs
categories: [m1ndbr34k_2024, Misc_m1ndbr34k_2024]
tags: [Misc]
image: '/assets/images/m1ndbr34k/logo.png'
---

## 𝄞 Introduction

![Intro](/assets/images/m1ndbr34k/Misc/OlderThanUs/intro.png)

## 𝄞 Solution

Un fichier **.txt** est mis à notre disposition. À l'intérieur, nous trouvons une longue chaîne de caractères.

![txt](/assets/images/m1ndbr34k/Misc/OlderThanUs/txt.png)

En décodant cette chaîne en **base64**, nous obtenons une série d'emojis !

![Cyberchef](/assets/images/m1ndbr34k/Misc/OlderThanUs/cyberchef.png)

```python 
🎌🙏🌒🥲🍈🙏🌒🥲🎌📕♏🐁🎈🙎♋🥱🎈🚏♏✊🎌🙏♏🥱🍈📕♏🥲🎈🙎♏🥲🎈🙏♋✊🎌🚏🌒🥱🍈🙏♏🐁🎌📕🌒🥱🎈🙎♋🥲🎌🚏♏✊🎈🚏♏🥱🍈📕♏🥲🎈🙎♏🐂🎌🙏♋🥲🎈🙏♏✊🍈🚏🌒🐂🎈📕♏🐁🎈🙎♋🥱🎌🚏🌒🏮🎌🙏♏🥱🍈📕🌒🥲🎈🚎♏🥲🎈🙏♋✊🎌🚏🌒🥱🍈🚏♏🥱🎈📔♏🥲🎈🚏♋🥱🎌🙏♏✊🍈🙏🌒🐂🎌📕♏🐂🎌🚎♏🐁🎈🙏♋✊🎈🚏🌒🐂🍈🙏🌒🥱🎈📔♏🐂🎌🙏♋🥱🎈🙏♏🏮🎌🙏♏🥱🍈📕🌒🐂🎌🙎♏🥲🎈🙏♋✊🎌🚏🌒🥱🍈🙏♏🐂🎌📕♏🥲🎈🙎♏🐁🎈🙏♋✊🎈🚏🌒🥲🍈🙏♏🐁🎌📕🌒🐂🎈🙎♏🥲🎈🙏♋✊🎈🙏♏🥲🍈🚏♏🥱🎈📔♏🐁🎌🙏🌎🥱🎈🚏♏✊🎈🚏♏🥱🍈📕🌒🐂🎈🙎♏🐁🎈🙏♋✊🎈🙏🌒🥱🍈🙏🌒🥱🎈📔♏🥲🎌🚏🌎🥲🎈🙏♏✊🍈🙏♏🐁🎌📕♏🐁🎈🙎♋🥲🎌🚏♏✊🎌🙏♏🥱🍈📕♏🐂🎌🚎♏🥲🎈🙏♋✊🎈🚏🌒🐂🍈🚏♏🥱🎈📔♏🐂🎌🚏♋🥲🎈🚏♏🏮🎈🚏♏🥱🍈📕🌒🐂🎈🙎♏🐁🎈🙏♋✊🎌🚏🌒🐁🍈🙏🌒🥱🎈📔♏🥱🎌🙏♋🥱🎈🚏♏✊🎌🙏♏🥱🍈📕♏🐂🎌🚎♏🥲🎈🙏♋✊🎌🚏🌒🥱🍈🚏♏🥱🎈📔♏🥲🎈🚏♋🥱🎌🙏♏✊🍈🙏🌒🐂🎌📕♏🐂🎌🚎♏🐁🎈🙏♋✊🎈🚏🌒🐂🍈🙏🌒🥱🎈📔♏🐂🎌🙏♋🥱🎈🚏♏✊🎌🙏♏🥱🍈📕🌒🐂🎌🙎♏🥲🎌🙏🌎🥲🎌🚏♏✊🎈🙏🌒🥱🍈🚏🌒🐂🎌📕🌒🥲🎈🚎♏🥲🎈🙏♋✊🎈🙏♏🥲🍈🙏🌒🐂🎌📕🌒🥱🎈🙎♋🥲🎌🚏🌒✊🎈🚏♏🥱🍈📕🌒🐂🎈🙎♏🐁🎈🙏♋✊🎌🚏♏🐁🍈🙏🌒🥱🎈📔♏🥱🎌🙏♋🥲🎈🙏♏✊🍈🚏♏🐁🎌📕♏🐁🎌🚎♏🥲🎈🙏♋✊🎈🚏🌒🐂🍈🚏♏🥱🎈📔♏🥲🎌🚏🌆☕
```

Cette chaîne semble être encodée en utilisant des emojis. Une simple recherche sur Google permet de trouver un dépôt [Github](https://github.com/keith-turner/ecoji). J'utilise une version en ligne de l'outil disponible à cette adresse [Ecoji.io](https://ecoji.io/).

![Ecoji](/assets/images/m1ndbr34k/Misc/OlderThanUs/ecoji.png)

Nous récupérons le binaire suivant : 

```
10101 01011 01000  00100 10000  00100 01000  11100 00101 10000  11100 01000  00100 11100 10000  11110 01000  01111 10000  10101 01000  11100 10000  01010 01000  01111 01111 10000  01111 01000  11100 00001 10000  11110 01000  11100 00111 00100 10000  01101 00101 11100 01000  00001 10000  10101 00100 01000  11100 10000  00100 01000  01111 10000  00101 01000  11100 10000  01111 01000  01111 10000  11110 10101 01000  11100 10000  11110 01000  00100 00100 10000  01111 01000  11100 10000  01010 01000  01111 01111 10000  01111 01000  11100 00100 10000  11110 01101 11100 00100 11111 10101 01000  00001 01111 10000  11110 01000  11100 10000  11010 01000  00100 10000  10101 01011 01000  01111 10000  01111
```

J'utilise le site [dcode.fr](https://www.dcode.fr/identification-chiffrement) pour identifier le chiffrement utilisé. Nous trouvons qu'il s'agit du code **Baudot**.

Il suffit maintenant de décoder notre chaîne !

![Baudot](/assets/images/m1ndbr34k/Misc/OlderThanUs/baudot.png)

𝄞 FLAG : `MB{TH3Y-4R3-N0T-G00D-1N-53CUR1TY-Y0U-D0NT-N33D-G00D-3NCRYPT10N-M3TH0D}` 𝄞