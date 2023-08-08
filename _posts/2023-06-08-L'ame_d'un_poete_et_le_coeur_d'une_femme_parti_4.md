---
title: L'âme d'un poète et le coeur d'une femme [4/4]
categories: [404CTF_2023, OSINT_404]
tags: [OSINT]
image: '/assets/images/404CTF_2023/404CTF.jpg'
---

## 𝄞 Introduction

![Intro](/assets/images/404CTF_2023/OSINT/L'ame_d'un_poete_et_le_coeur_d'une_femme_parti_4/intro.png)


## 𝄞 Solution

L'objectif de ce challenge est de **trouver la réponse aux différentes questions posées sur le serveur Discord.**

### 𝄞𝄞 Première Question : 

![Question_1](/assets/images/404CTF_2023/OSINT/L'ame_d'un_poete_et_le_coeur_d'une_femme_parti_4/1.png)

Pour répondre à cette première question, j'ai effectué une recherche sur internet en utilisant un fragment de la question, **"promeneur inoccupé qui, sortant du jardin des Tuileries"**. J'ai rapidement trouvé un texte de **Louise Colet** intitulé [Un drame dans la rue de Rivoli](https://fr.wikisource.org/wiki/Un_drame_dans_la_rue_de_Rivoli/1).

![Flag1](/assets/images/404CTF_2023/OSINT/L'ame_d'un_poete_et_le_coeur_d'une_femme_parti_4/flag1.png)

𝄞 FLAG_1 : `1835` 𝄞

### 𝄞𝄞 Deuxième Question : 

![Question_2](/assets/images/404CTF_2023/OSINT/L'ame_d'un_poete_et_le_coeur_d'une_femme_parti_4/2.png)

Pour la deuxième question, j'ai utilisé une approche similaire en cherchant **une partie du poème sur Google** dans le but de trouver le poème original. Cependant, cela n'a pas été fructueux. J'ai alors réfléchi à la logique de la situation et me suis dit qu'il s'agissait probablement d'un poème de **Louise Colet**. J'ai finalement trouvé ce [site](https://www.persee.fr/doc/grif_0770-6081_1975_num_7_1_1458) qui contenait le poème en question qui est **l'anticréation**.

![Flag_2](/assets/images/404CTF_2023/OSINT/L'ame_d'un_poete_et_le_coeur_d'une_femme_parti_4/flag2.png)

𝄞 FLAG_2 : `Pour nous, aimer et croire Au bonheur nous conduit. Coule une vie obscure Que le devoir remplit; L'onde à l'ombre est plus pure, Rien ne trouble son lit.` 𝄞


### 𝄞𝄞 Dernière Question :

![Question_3](/assets/images/404CTF_2023/OSINT/L'ame_d'un_poete_et_le_coeur_d'une_femme_parti_4/3.png)

La dernière question s'est avérée plus difficile que je ne le pensais. J'ai consacré près d'une heure et trente minutes à chercher des informations sur la rencontre entre **Louise Colet et Victor Hugo**. Après tout ce temps investi, j'ai finalement trouvé ce [site](https://gallica.bnf.fr/ark:/12148/bpt6k8572147/f7.item).


![Flag_3](/assets/images/404CTF_2023/OSINT/L'ame_d'un_poete_et_le_coeur_d'une_femme_parti_4/flag3.png)

𝄞 FLAG_3 : `404CTF{Guernesey_1857}` 𝄞

## 𝄞 Conclusion
Ce dernier défi de la série **L'âme d'un poète et le coeur d'une femme** m'a vraiment mis à l'épreuve. J'ai dû faire preuve de persévérance et de patience pour trouver les réponses aux questions posées sur le serveur Discord.
























