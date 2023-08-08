---
title: ASCON Marchombre
categories: [404CTF_2023, Cryptographie_404]
tags: [Cryptographie, ascon]
image: '/assets/images/404CTF_2023/404CTF.jpg'
---

## 𝄞 Introduction

![Intro](/assets/images/404CTF_2023/Cryptographie/Ascon_marchombre/intro.png)


## 𝄞 Solution

L'objectif de ce challenge est de **déchiffrer** le message chiffré en utilisant **l'algorithme ASCON**.

### 𝄞𝄞 Algorithme ASCON
**ASCON** *(Advanced Symmetric Core)* est un **algorithme** de chiffrement **symétrique** à clé secrète. Il est conçu pour offrir une sécurité élevée tout en étant efficace en termes de performances. Pour plus de détails, consultez ce [lien](https://en.wikipedia.org/wiki/Ascon_(cipher))

Tous les éléments de l'énoncé nous permettent de créer un script en python pour décoder le message chiffré. Nous allons utiliser la bibliothèque [ascon](https://pypi.org/project/ascon/).

```python
import ascon

def decrypt_ascon(key, nonce, associated_data, ciphertext):
    plaintext = ascon.decrypt(key.to_bytes(16, 'big'), nonce.to_bytes(16, 'big'), associated_data, ciphertext)
    return plaintext

# Clé (en hexadécimal)
key = int("00456c6c616e61206427416c2d466172", 16)
# Nonce (en entier)
nonce = 0
# Données associées (en hexadécimal)
associated_data = bytes.fromhex("80400c0600000000")
# Message chiffré (en hexadécimal)
ciphertext = bytes.fromhex("ac6679386ffcc3f82d6fec9556202a1be26b8af8eecab98783d08235bfca263793b61997244e785f5cf96e419a23f9b29137d820aab766ce986092180f1f5a690dc7767ef1df76e13315a5c8b04fb782")

plaintext = decrypt_ascon(key, nonce, associated_data, ciphertext)
print("Message déchiffré:", plaintext.hex())
```
![Decrypt](/assets/images/404CTF_2023/Cryptographie/Ascon_marchombre/decrypt.png)

Le résultat obtenu est  
`4c6120766f6965206465206c276f6d6272650a45742064752073696c656e63650a3430344354467b563372355f6c345f6c756d31e872332e7d0a456c6c616e61`
Il suffit maintenant de décoder le resultat qui est en hexadecimal.

![Flag](/assets/images/404CTF_2023/Cryptographie/Ascon_marchombre/flag.png)

𝄞 FLAG : `404CTF{V3r5_l4_lum1èr3.}` 𝄞

## 𝄞 Conclusion
Dans ce défi, nous avons utilisé l'algorithme ASCON pour déchiffrer un message chiffré. ASCON est un algorithme de chiffrement symétrique à clé secrète qui offre à la fois sécurité et efficacité en termes de performances. En utilisant la bibliothèque ascon, nous avons réussi à décoder le message et obtenir le résultat en format hexadécimal.