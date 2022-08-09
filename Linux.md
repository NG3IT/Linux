# Linux administration

---

<br>

## Summary

- [Help](https://github.com/NG3IT/Linux/blob/main/Linux.md#help)
- [Filesystem](https://github.com/NG3IT/Linux/blob/main/Linux.md#filesystem)
- [Les permissions des fichiers et des répertoires](https://github.com/NG3IT/Linux/blob/main/Linux.md#les-permissions-des-fichiers-et-des-r%C3%A9pertoires)
- [Sudo et su (switch user)](https://github.com/NG3IT/Linux/blob/main/Linux.md#sudo-et-su-switch-user)
- [iostat](https://github.com/NG3IT/Linux/blob/main/Linux.md#iostat)
- [Vi/Vim](https://github.com/NG3IT/Linux/blob/main/Linux.md#vivim)
- [Utilisateurs et groupes](https://github.com/NG3IT/Linux/blob/main/Linux.md#utilisateurs-et-groupes)

---

<br>

## Help

```bash
# Manuel
$ man <command>
# Obtenir les raccourcis -> h | H

# Manuel avec pattern
$ man -k <pattern>
$ man -k memory

# Navigation
/<pattern> -> Recherche un pattern
n -> Prochaine occurence
N -> Précédente occurence
G -> Bas de page
g -> Début de page
```

<br>

---

<br>

## Filestystem

Filesystem Hierarchy Standard (FHS) : standard Linux (v3 date de 2015)

### Hiérarchie du système de fichier

```bash
# Utile pour le boot
/boot
# Binaires
/bin
# Binaires administrateurs
/sbin
# Périphériques physiques ou virtuels
/dev
# Configuration
/etc
# Ensemble des home
/home
# Librairies
/lib
# Programmes optionnels
/opt
# Home de root
/root
# Répertoire de binaire "non nécessaire au système" (Unix System Resources) 
/usr
# Données (logs, bdd, etc.)
/var
# Temporaire
/tmp
# Information spécifiques du noyau/système
/proc
# Information spécifiques du noyau/système
/sys
# Récupération de fs
/lost+found
# Montages temporaires
/mnt
# Montages temporaires
/media
```

<br>

### ls - list directory content

```bash
# Afficher les fichiers cachés
$ ls -la 
# Classer par date de modification
$ ls -lt
# Human readable 
$ ls -lh
# Mode liste avec seulement le nom
$ ls -1
# Du plus récent au plus récent
$ ls -larth
```

<br>

### cd - change directory

```bash
# Répertoire home
$ cd
$ cd ~
# Répertoire parent
$ cd ..
```

<br>

---

<br>

## Les permissions des fichiers et des répertoires

```bash
# Afficher les permissions
$ getfacl <file>
$ stat <file>
```

<br>

### Signification rwx/421

```bash
# r : read
# w : write
# x : executable

# 4 : read
# 2 : write
# 1 : executable
```

<br>

### Changement de droits

```bash
# Lecture et écriture uniquement pour le propriétaire
$ chmod 600 <file> 

# Application récursive
$ chmod -R 774 <directory>

# Application des droits en rwx
# chmod ugo+rwx <file>
# chmod o-x <file>
```

<br>

### Changement de propriétaire et de groupe

```bash
# Changement de propriétaire
$ chown <user> <file>
# Changement récursif de propriétaire
$ chown -R <user> <directory>

# Changement de propriétaire et de groupe
$ chown <user>:<group> <file>
```

<br>

### Signification du premier caractère

```bash
# - : file
# d : directory
# c : character device
# l : symlink
# p : named pipe
# s : socket
# b : block device
# D : door
```

<br>

---

<br>

## Sudo et su (switch user)

```bash
# Fichier de configuration
/etc/sudoers ou /etc/sudoers.d/*

# Utilisation de sudo
$ sudo <command>

# Utilisation d'un user spécifique
$ sudo -u <user> <command>

# Afficher les autorisation sudo
$ sudo -l
```

<br>

```bash
# Changement d'utilisateur avec son environnement
$ su - <user>

# Changement avec l'utilisateur root
$ su -

# Exécution d'une commande en tant qu'un autre utilisateur
$ su - <user> -c "<command>"
```

<br>

---

<br>

## Utilisateurs et groupes

UID -> User ID

```bash
# UID
# 0 -> root
# 0 - 100 -> uid statique réservés pour le système
# > 1000 -> uid dynamique réservés pour le système
# < 1000 -> autres
# nobody -> 

# Lister les utilisateurs
$ cat /etc/passwd
$ getent passwd
$ compgen -u

# Ajouter un utilisateur
$ useradd <'utilisateur
$ useradd -s <shell> -c <commentaire> -d <home> -g <groupe> -G <groupas_additionnels> -k <skelette>
$ passwd <utilisateur>

# Fichier de configuration de useradd
$ cat /etc/default/useradd

# Créer des utilisateurs en cascade (ajout dans /etc/passwd)
$ newusers

# Supprimer un utilisateur
$ deluser <user>
$ deluser --remove-home

# Gestion des utilisateurs
# Statut de l'utilisateur
$ passwd -S <utilisateur>
# Force l'expiration du mot de passe
$ passwd -e <utilisateur>
# Locker un utilisateur
$ passwd -l <utilisateur>
# Unlocker un utilisateur
$ password -u <utilisateur>
```

Mot de passe

```bash
# Exemple
$ openssl <mode> <encodage> <nombre_de_caractères>
$ openssl rand -base64 12
```


GID -> Group ID

```bash
# GID
# 0 -> root
# 100 -> groupe par défault "users"
# < 1000 -> groupes utilisateurs

# Lister les groupes
$ cat /etc/group
$ getent group

# Ajouter des groupes
$ groupadd <groupe>
# Forcer le GID
$ groupadd -g <GID> <groupe>
# Créer un groupe système
$ groupadd -r <groupe>

# Supprimer des groupe
$ groupdel <groupe>

# Changer le groupe auquel appartient un fichier
$ chgrp <groupe> <fichier>

# Ajouter un utilisateur à un groupe
$ usermod -aG <groupe> <utilisateur>
```

<br>

---

<br>

## iostat

```bash
$ iostat
$ iostat -h
# Afficher l'heure
$ iostat -t

# Rafraichissement
$ iostat <secondes>
$ iostat 2

# CPU
$ iostat -c

# Devices
$ iostat -d
# Spécifier un device
$ iostat -p <device>
$ iostat -p sda

# Spécifier une période de temps pour analyse
$ iostat 3 5
```

<br>

---

<br>

## Sauvegarde et restauration d'un disque (dd)

```bash
# Copie d'un disque vers un autre
$ dd if=<disque> of=<disque> status=progress
$ dd if=/dev/sdb of=/dev/sdc status=progress

# Copie d'un disque vers un fichier image
$ dd if=<disque> of=<image> status=progress
$ dd if=/dev/sdb of=image.img status=progress
$ dd if=image.img of=/dev/sdb status=progress
```

<br>

---

<br>

## Cleaner un disque (dd)

```bash
# Démonter le volume avant le clean de préférence
$ dd if=/dev/zero of=/dev/sdb status=progress
$ dd if=/dev/random of=/dev/sdb status=progress
```

<br>

---

<br>

## Vi/Vim

```bash
# Mode
i -> Insert mode
escap -> Classic mode
Ctrl + V -> Visual mode

# Sauvegarder et quitter le fichier
:wq
# Quitter sans sauvegarder
:q!

# Déplacement à la première ligne
gg
# Déplacement à la dernière ligne
G

# Recherche de patterns
/<pattern>
# Pattern suivant
n

# Afficher les numéros de lignes
:set number
# Déplacement vers une ligne spécifique
:<numéro_de_ligne>
# Ouvrir le fichier à une ligne spécifique
# Vim +10 <file>

# Annuler l'action précédente
:undo
# Rejouer l'action précédente
:redo

# Copier une ligne
yy
# Coller une ligne
p
# Copier un ensemble de lignes
<nombre_de_lignes>yy
4yy
# Copier un ensemble de lignes spécifiques
:<première_ligne>,<dernière_ligne>y
:11,15y

# Suppression de la ligne
dd 
# Suppression d'une ligne spécifique
dd +<numéro_de_ligne>
dd +10

# Remplacement d'un pattern
:s/<pattern_à_remplacer>/<nouveau_pattern>/g
# Remplacement de plusieurs patterns
:%s/<patterns_à_remplacer>/<nouveaux_patterns>/g

# Modification de plusieurs lignes
# Visual mode
Ctrl + v
# Sélectionner les valeurs/lignes
# Shift + i
# Faire les modifications
# Echap
```

<br>

---

<br>

##
