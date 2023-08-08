---
title: Je veux la lune !
categories: [404CTF_2023, Exploitation binaire_404]
tags: [injection de commande]
image: '/assets/images/404CTF_2023/404CTF.jpg'
---

## 𝄞 Introduction

![Intro](/assets/images/404CTF_2023/Exploitation_binaire/Je_veux_la_lune/intro.png)


## 𝄞 Solution

L'objectif de ce challenge est de trouver un moyen d'afficher le contenu du fichier lune.txt.

### 𝄞𝄞 Script

```bash
#!/bin/bash

Caligula=Caius

listePersonnes="Cherea Caesonia Scipion Senectus Lepidus Caligula Caius Drusilla"

echo "Bonjour Caligula, ceci est un message de Hélicon. Je sais que les actionnaires de ton entreprise veulent se débarrasser de toi, je me suis donc dépêché de t'obtenir la lune, elle est juste là dans le fichier lune.txt !

En attendant j'ai aussi obtenu des informations sur Cherea, Caesonia, Scipion, Senectus, et Lepidus, de qui veux-tu que je te parle ?"
read personne
eval "grep -wie ^$personne informations.txt"

while true; do
    echo "
De qui d'autre tu veux que je te parle ?"
    read personne

    if [ -n $personne ] && [ $personne = "stop" ] ; then
    exit
    fi

    bob=$(grep -wie ^$personne informations.txt)
    
    if [ -z "$bob" ]; then
        echo "Je n'ai pas compris de qui tu parlais. Dis-moi stop si tu veux que je m'arrête, et envoie l'un des noms que j'ai cités si tu veux des informations."
    else
        echo $bob
    fi  

done
```
Le script fourni **recherche les lignes contenant le mot contenu dans la variable $personne dans le fichier informations.txt**. Le problème est qu'il n'y a **pas de vérification** sur les valeurs passées à la variable **$personne**. Nous allons donc pouvoir effectuer une **injection de commande**.

### 𝄞𝄞 Netcat

Une fois connecté au service, nous allons essayer d'afficher **toutes les lignes** du fichier **informations.txt** en utilisant `.*`.

![Information](/assets/images/404CTF_2023/Exploitation_binaire/Je_veux_la_lune/information.png)

Comme nous pouvons le voir ici, nous n'avons rien d'intéressant.
Nous allons donc essayer d'ajouter une autre commande en utilisant l'opérateur *(|, &&, ;)* pour afficher le contenu du fichier **lune.txt**.

![Flag1](/assets/images/404CTF_2023/Exploitation_binaire/Je_veux_la_lune/flag1.png)
`fxoverflow informations.txt | cate lune.txt`

𝄞 FLAG : `404CTF{70n_C0EuR_v4_7e_1Ach3R_C41uS}` 𝄞

## 𝄞 Conclusion
Ce défi nous a permis de mettre en pratique nos compétences injection de commandes. En exploitant une vulnérabilité dans le script fourni, nous avons pu exécuter une commande pour afficher le contenu du fichier lune.txt.

