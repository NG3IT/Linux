# Linux administration

---

<br>

## Summary

- [Help](https://github.com/NG3IT/Linux/blob/main/Linux.md#help)
- [Filesystem](https://github.com/NG3IT/Linux/blob/main/Linux.md#filesystem)
- [Les permissions des fichiers et des répertoires](https://github.com/NG3IT/Linux/blob/main/Linux.md#les-permissions-des-fichiers-et-des-r%C3%A9pertoires)

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
