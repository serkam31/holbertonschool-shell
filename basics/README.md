# Shell Basics

Ce dossier contient 18 scripts qui couvrent les commandes de base du Shell pour naviguer et manipuler le système de fichiers Unix/Linux.

## Objectifs d'apprentissage

- Comprendre la structure du système de fichiers Unix
- Naviguer efficacement dans les dossiers
- Manipuler fichiers et répertoires
- Utiliser les options avancées des commandes de base

---

## Liste des Scripts

### 0-current_working_directory
**Commande** : `pwd`

**Description** : Affiche le chemin absolu du répertoire de travail actuel (Present Working Directory).

**Concept** : Savoir où vous vous trouvez dans l'arborescence du système de fichiers.

**Exemple de sortie** :
```
/home/user/holbertonschool-shell/basics
```

---

### 1-listit
**Commande** : `ls`

**Description** : Liste le contenu du répertoire courant (fichiers et dossiers visibles).

**Concept** : Visualiser les fichiers dans un dossier.

---

### 2-bring_me_home
**Commande** : `cd ~` ou `cd`

**Description** : Change le répertoire courant vers le répertoire personnel de l'utilisateur (home directory).

**Concept** : Navigation rapide vers votre dossier utilisateur.

---

### 3-listfiles
**Commande** : `ls -l`

**Description** : Affiche le contenu du répertoire en format long (détails sur les permissions, propriétaire, taille, date).

**Concept** : Obtenir des informations détaillées sur les fichiers.

**Exemple de sortie** :
```
-rw-r--r-- 1 user user 1234 Jan 21 10:00 file.txt
drwxr-xr-x 2 user user 4096 Jan 21 09:00 folder
```

---

### 4-listmorefiles
**Commande** : `ls -la`

**Description** : Liste TOUS les fichiers (y compris les fichiers cachés commençant par `.`) en format long.

**Concept** : Les fichiers cachés sont souvent des fichiers de configuration (`.bashrc`, `.gitignore`, etc.).

---

### 5-listfilesdigitonly
**Commande** : `ls -ln`

**Description** : Liste les fichiers en format long avec les UID (User ID) et GID (Group ID) numériques au lieu des noms.

**Concept** : Comprendre que les utilisateurs et groupes sont identifiés par des numéros dans le système.

---

### 6-firstdirectory
**Commande** : `mkdir /tmp/my_first_directory`

**Description** : Crée un nouveau répertoire nommé `my_first_directory` dans `/tmp`.

**Concept** : Création de dossiers avec `mkdir`.

---

### 7-movethatfile
**Commande** : `mv /tmp/betty /tmp/my_first_directory/`

**Description** : Déplace le fichier `betty` vers le dossier `my_first_directory`.

**Concept** : `mv` sert à déplacer ET à renommer des fichiers.

---

### 8-firstdelete
**Commande** : `rm /tmp/my_first_directory/betty`

**Description** : Supprime le fichier `betty`.

**Concept** : Suppression de fichiers avec `rm` (attention : pas de corbeille !).

---

### 9-firstdirdeletion
**Commande** : `rmdir /tmp/my_first_directory`

**Description** : Supprime le répertoire `my_first_directory` (doit être vide).

**Concept** : `rmdir` supprime uniquement les dossiers vides. Pour les dossiers non vides, utilisez `rm -r`.

---

### 10-back
**Commande** : `cd -`

**Description** : Retourne au répertoire précédent.

**Concept** : Navigation rapide entre deux dossiers avec `-`.

---

### 11-lists
**Commande** : `ls -la . .. /boot`

**Description** : Liste le contenu de trois emplacements :
- `.` (répertoire courant)
- `..` (répertoire parent)
- `/boot` (dossier système)

**Concept** : `.` et `..` sont des références spéciales dans Unix.

---

### 12-file_type
**Commande** : `file /tmp/iamafile`

**Description** : Affiche le type du fichier `iamafile`.

**Concept** : `file` détecte le type de contenu d'un fichier (texte, binaire, image, etc.).

**Exemple de sortie** :
```
/tmp/iamafile: ASCII text
```

---

### 13-symbolic_link
**Commande** : `ln -s /bin/ls __ls__`

**Description** : Crée un lien symbolique nommé `__ls__` pointant vers `/bin/ls`.

**Concept** : Un lien symbolique est un raccourci vers un autre fichier. Modifier le lien ne modifie pas l'original.

---

### 14-copy_html
**Commande** : `cp -u *.html ..`

**Description** : Copie tous les fichiers HTML du répertoire courant vers le répertoire parent, uniquement s'ils sont plus récents ou inexistants.

**Concept** : L'option `-u` (update) évite de copier des fichiers plus anciens.

---

### 15-lets_move
**Commande** : `mv [[:upper:]]* /tmp/u`

**Description** : Déplace tous les fichiers dont le nom commence par une majuscule vers `/tmp/u`.

**Concept** : Utilisation des patterns (wildcards) et des classes de caractères `[[:upper:]]`.

---

### 16-clean_emacs
**Commande** : `rm *~`

**Description** : Supprime tous les fichiers se terminant par `~` (fichiers de backup Emacs).

**Concept** : Nettoyage de fichiers temporaires avec des patterns.

---

### 17-tree
**Commande** : `mkdir -p welcome/to/school`

**Description** : Crée une arborescence de répertoires imbriqués en une seule commande.

**Concept** : L'option `-p` (parents) crée tous les dossiers intermédiaires nécessaires.

---

## Commandes Clés Apprises

| Commande | Description |
|----------|-------------|
| `pwd` | Affiche le répertoire courant |
| `ls` | Liste les fichiers |
| `cd` | Change de répertoire |
| `mkdir` | Crée un répertoire |
| `rmdir` | Supprime un répertoire vide |
| `rm` | Supprime un fichier |
| `mv` | Déplace ou renomme un fichier |
| `cp` | Copie un fichier |
| `file` | Affiche le type d'un fichier |
| `ln -s` | Crée un lien symbolique |

## Options Importantes

- `-l` : Format long (détails)
- `-a` : Afficher les fichiers cachés
- `-n` : Afficher les UID/GID numériques
- `-u` : Mode update (copie uniquement si plus récent)
- `-p` : Créer les dossiers parents si nécessaire
- `-r` : Récursif (pour parcourir les sous-dossiers)

## Concepts Clés

1. **Chemins absolus vs relatifs** :
   - Absolu : `/home/user/file.txt` (commence par `/`)
   - Relatif : `../documents/file.txt` (relatif au dossier courant)

2. **Répertoires spéciaux** :
   - `.` = répertoire courant
   - `..` = répertoire parent
   - `~` = répertoire personnel (home)
   - `-` = répertoire précédent

3. **Wildcards (jokers)** :
   - `*` = n'importe quelle chaîne de caractères
   - `?` = un seul caractère
   - `[abc]` = un caractère parmi a, b, ou c
   - `[[:upper:]]` = n'importe quelle majuscule

4. **Fichiers cachés** :
   - Commencent par `.` (exemple : `.bashrc`, `.gitignore`)
   - Non affichés par `ls` par défaut (utilisez `ls -a`)

## Ressources

- `man ls` : Manuel de la commande ls
- `man cd` : Manuel de la commande cd
- `man pwd` : Manuel de la commande pwd
