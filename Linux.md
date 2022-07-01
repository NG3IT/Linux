# Linux administration

---

<br>

## Summary

- Help
- Filesystem
-

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

