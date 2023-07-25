---
title: Les Mystères du cluster de la Comtesse de Ségur
categories: [404CTF_2023, Forensic_404]
tags: [Cloud]
---

## 𝄞 Introduction

Nous avons à notre disposition un fichier au format **zip** à analyser.
![Intro](/assets/images/404CTF_2023/Forensic/Les_Mystères_du_cluster_de_la_Comtesse_de_Ségur/intro.png)

## 𝄞 Solution
La première étape consiste à analyser le contenu du fichier **zip**. En l'ouvrant, nous trouvons plusieurs fichiers. Notre objectif est de trouver des informations utiles parmi ces fichiers.

![File](/assets/images/404CTF_2023/Forensic/Les_Mystères_du_cluster_de_la_Comtesse_de_Ségur/file.png)

Après avoir examiné attentivement les fichiers, j'ai identifié un fichier particulièrement intéressant : **io.kubernetes.cri-o.LogPath**. Ce fichier est utilisé pour stocker les journaux des conteneurs exécutés par *CRI-O*.

Pour extraire les informations de ce fichier, nous utilisons la commande strings :
```bash
strings io.kubernetes.cri-o.LogPath 
```

![Flag](/assets/images/404CTF_2023/Forensic/Les_Mystères_du_cluster_de_la_Comtesse_de_Ségur/flag.png)

J'ai reconstitué la commande 
```bash
curl https://agent.challenges.404ctf.fr/ -o agent.zip
```

![Flag2](/assets/images/404CTF_2023/Forensic/Les_Mystères_du_cluster_de_la_Comtesse_de_Ségur/flag2.png)

𝄞 FLAG : `404CTF{K8S_checkpoints_utile_pour_le_forensic}` 𝄞

## 𝄞 Conclusion

En résolvant le défi "Les Mystères du cluster de la Comtesse de Ségur", nous avons analysé un fichier zip contenant plusieurs fichiers. En examinant les informations contenues dans ces fichiers, nous avons découvert une commande curl qui nous a permis de récupérer un autre fichier zip. Cette résolution met en évidence l'importance de l'analyse minutieuse des fichiers et de l'exécution des commandes appropriées pour progresser dans le défi.