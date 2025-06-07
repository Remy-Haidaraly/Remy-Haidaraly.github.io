---
title: FxGuitarPro
categories: [m1ndbr34k_2025, Reverse_m1ndbr34k_2025]
tags: [Reverse]  
image: '/assets/images/m1ndbr34k/logo.png'
---

## 𝄞 Introduction

![Intro](/assets/images/m1ndbr34k_2025/Reverse/FxGuitarPro/intro.png)

> Votre ami guitariste a perdu la clé de licence du logiciel FxGuitarPro... Problème : il a un concert dans 3 jours et toutes ses compositions sont stockées dans ce logiciel. Il vous a donc demandé de l'aider à retrouver sa clé de licence !
{: .prompt-tip }
---

## Readme.txt 
```python
README.txt

Aucune stéganographie n'est à effectuer sur les images : elles sont uniquement nécessaires au bon fonctionnement du logiciel.

Votre objectif est de comprendre le fonctionnement de l'algorithme de génération de la clé de licence, afin de retrouver celle de votre ami !

Vous pouvez tester votre réponse directement dans le logiciel pour vérifier si vous avez trouvé la bonne clé de licence ou non.


PS : Le premier groupe qui trouve le flag est prié de m’envoyer un message privé sur Discord : fxoverflow
(Des petits chocolats vous attendent ! :)
```

## La facture : 
![facture](/assets/images/m1ndbr34k_2025/Reverse/FxGuitarPro/facture.webp)

## 𝄞𝄞 Solution

Pour résoudre ce challenge, nous pouvons essayer de reverse le fichier .exe mais cela s'avère être trop complexe… il va falloir être plus stratège !

On peut essayer d’en découvrir plus sur le binaire

```python
strings {binaire}
```
![string](/assets/images/m1ndbr34k_2025/Reverse/FxGuitarPro/strings.webp)
![string1](/assets/images/m1ndbr34k_2025/Reverse/FxGuitarPro/strings2.webp)
![string2](/assets/images/m1ndbr34k_2025/Reverse/FxGuitarPro/strings3.webp)

Il devient alors possible de récupérer le code source à partir de cet exécutable. Une simple recherche sur Internet permet de découvrir des outils adaptés à cette tâche.

![google](/assets/images/m1ndbr34k_2025/Reverse/FxGuitarPro/google.webp)

Une rapide recherche permet de découvrir l’outil **pyinstxtractor** :

```python
python3 pyinstxtractor.py ../FxGuitarPro.exe
```

![python3](/assets/images/m1ndbr34k_2025/Reverse/FxGuitarPro/python3.webp)

Cela génère un dossier avec plusieurs fichiers, dont des fichiers .**pyc**. On trouve ainsi le fichier **FxGuitarPro.pyc**. 

On découvre alors qu’il faut utiliser un décompilateur pour lire le contenu des fichiers `.pyc`.
C’est aussi l’occasion pour les joueurs de comprendre ce qu’est un **bytecode Python**.
Malheureusement, de nombreux décompilateurs classiques (comme **uncompyle6** ou **decompyle3**) ne prennent pas encore en charge la version **3.13.3 de Python**.

En effectuant une simple recherche Google, on tombe sur le site **PyLingual** :
![python3](/assets/images/m1ndbr34k_2025/Reverse/FxGuitarPro/google2.webp)

On y téléverse le fichier .pyc extrait précédemment grâce à **pyinstxtractor**.

![pylingual](/assets/images/m1ndbr34k_2025/Reverse/FxGuitarPro/pylingual.webp)

![pylingual2](/assets/images/m1ndbr34k_2025/Reverse/FxGuitarPro/pylingual2.webp)

Grâce à PyLingual, on récupère le code source original de l’application :

![code](/assets/images/m1ndbr34k_2025/Reverse/FxGuitarPro/code.webp)

On découvre alors l’algorithme utilisé pour générer les clés de licence :
repose sur **une date** et un **secret token.**

## Reconstitution de la clé

- **Secret token** : `FxGuitar`
- **Date d’achat** (présente sur la facture) : `2025-03-13`
- Format attendu : celui de `datetime.now()` (sans espaces, sans séparateurs entre les deux parties)

![FxguitarPro_solve](/assets/images/m1ndbr34k_2025/Reverse/FxGuitarPro/FxGuitarPro.webp)

Je peux maintenant valider mon flag.

𝄞 FLAG : `MB{2025-03-13FxGuitar}`𝄞