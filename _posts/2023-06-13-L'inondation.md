---
title: L'Inondation
categories: [404CTF_2023, Programmation]
tags: [Python, netcat, programmation]
---

## 𝄞 Introduction

![Intro](/assets/images/404CTF_2023/Programmation/L'inondation/intro.png)


## 𝄞 Solution

L'objectif de ce challenge est de trouver un moyen de **compter** le nombre de **rhinocéros** le plus rapidement possible !

![Nc](/assets/images/404CTF_2023/Programmation/L'inondation/nc1.png)

Nous avons une image avec un motif qui se répète : `~c°^)`.
Si nous fournissons une réponse incorrecte, la connexion est interrompue.
Si nous ne répondons pas, un minuteur s'active et nous envoie un message avant de couper la connexion

![Nc2](/assets/images/404CTF_2023/Programmation/L'inondation/nc2.png)


Pour résoudre ce challenge, il suffit de développer un **script** qui se connecte au serveur Netcat et compte le nombre de rhinocéros pour chaque image. Cependant, j'ai compliqué les choses en utilisant un script plus complexe alors qu'il y avait une solution plus simple notament en utilisé une librairie comme **pwntool**.

## 𝄞𝄞 Script python pas optimisé 

```python
import socket

host = 'challenges.404ctf.fr'
port = 31420
buffer_size = 4096

# Création d'une socket
client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

try:
    # Connexion au serveur
    client_socket.connect((host, port))
    print("Connecté au serveur")

    # Répéter le processus 99 fois
    for _ in range(100):
        # Recevoir la réponse du serveur
        response = b""
        while True:
            data = client_socket.recv(buffer_size)
            response += data
            if response.endswith(b"> "):
                break

        response = response.decode()
        print("Réponse du serveur pour l'itération", _ + 1, ":\n", response)

        # Envoyer la réponse
        solve = response.count("~c`°^)")
        print(solve)

        reply = str(solve).encode() + b'\n' # sans le \n --> reponse s'envoie pas 
        client_socket.send(reply)
        print("Réponse envoyée avec succès")

    # Récupérer et afficher la réponse du serveur pour la 100e itération
    response = b""
    while True:
        data = client_socket.recv(buffer_size)
        response += data
        if not data:
            break

    response = response.decode()
    print("Réponse du serveur pour la 100e itération :\n", response)

finally:
    # Fermer la connexion
    client_socket.close()
```

![Flag](/assets/images/404CTF_2023/Programmation/L'inondation/flag.png)

𝄞 FLAG : `404CTF{4h,_l3s_P0uvo1rs_d3_l'iNforM4tiqu3!}` 𝄞 


## 𝄞 Conclusion
Ce défi nous a permis de mettre en pratique nos compétences en programmation Python et en communication avec des sockets. En développant un script pour compter le nombre de rhinocéros dans les images fournies par le serveur Netcat, nous avons pu obtenir le flag avec succès.

