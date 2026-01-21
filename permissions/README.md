# Shell Permissions

Ce dossier contient 17 scripts qui couvrent le système de permissions Unix/Linux, la gestion des utilisateurs, des groupes et de la propriété des fichiers.

## Objectifs d'apprentissage

- Comprendre le système de permissions Unix (lecture, écriture, exécution)
- Maîtriser les commandes de gestion des permissions
- Gérer les propriétaires et groupes de fichiers
- Utiliser les permissions en notation symbolique et octale

---

## Le Système de Permissions Unix

Chaque fichier et répertoire possède :
- Un **propriétaire** (user/owner)
- Un **groupe** (group)
- Des **permissions** pour trois catégories :
  - **u** (user) : le propriétaire
  - **g** (group) : le groupe
  - **o** (others) : les autres utilisateurs

Les permissions possibles sont :
- **r** (read) : lecture = 4
- **w** (write) : écriture = 2
- **x** (execute) : exécution = 1

Exemple :
```
-rwxr-xr--  1 user group  1234 Jan 21 10:00 file.txt
│││││││││
││││││││└─ autres : r-- (lecture seule) = 4
│││││││└── groupe : r-x (lecture + exécution) = 5
││││││└─── propriétaire : rwx (tout) = 7
│││││└──── nombre de liens
││││└───── groupe propriétaire
│││└────── utilisateur propriétaire
││└─────── taille en octets
│└──────── type : - (fichier), d (dossier), l (lien)
```

---

## Liste des Scripts

### 0-iam_betty
**Commande** : `su betty`

**Description** : Change l'utilisateur courant en `betty`.

**Concept** : `su` (switch user) permet de changer d'utilisateur. Nécessite le mot de passe de betty.

---

### 1-who_am_i
**Commande** : `whoami`

**Description** : Affiche le nom de l'utilisateur actuellement connecté.

**Concept** : Vérifier votre identité actuelle dans le système.

**Exemple de sortie** :
```
root
```

---

### 2-groups
**Commande** : `groups`

**Description** : Affiche tous les groupes auxquels appartient l'utilisateur courant.

**Concept** : Les groupes définissent des ensembles d'utilisateurs partageant certains droits d'accès.

**Exemple de sortie** :
```
user sudo docker
```

---

### 3-new_owner
**Commande** : `chown betty hello`

**Description** : Change le propriétaire du fichier `hello` pour l'utilisateur `betty`.

**Concept** : `chown` (change owner) modifie le propriétaire d'un fichier. Nécessite généralement les droits root/sudo.

**Syntaxe** : `chown [nouvel_utilisateur] [fichier]`

---

### 4-empty
**Commande** : `touch hello`

**Description** : Crée un fichier vide nommé `hello`.

**Concept** : `touch` crée un fichier vide ou met à jour la date de modification d'un fichier existant.

---

### 5-execute
**Commande** : `chmod u+x hello`

**Description** : Ajoute la permission d'exécution pour le propriétaire du fichier `hello`.

**Concept** :
- `chmod` = change mode (modifier les permissions)
- `u` = user (propriétaire)
- `+x` = ajouter (+) l'exécution (x)

---

### 6-multiple_permissions
**Commande** : `chmod ug+x,o+r hello`

**Description** : Ajoute :
- Exécution pour le propriétaire (u) et le groupe (g)
- Lecture pour les autres (o)

**Concept** : On peut modifier plusieurs permissions en une seule commande, séparées par des virgules.

---

### 7-everybody
**Commande** : `chmod ugo+x hello` ou `chmod a+x hello`

**Description** : Ajoute la permission d'exécution pour tout le monde (all).

**Concept** : `a` = all = ugo (tout le monde).

---

### 8-James_Bond
**Commande** : `chmod 007 hello`

**Description** : Définit les permissions à `-------rwx` (007 en octal).
- Propriétaire : aucune permission (0)
- Groupe : aucune permission (0)
- Autres : toutes les permissions (7 = rwx)

**Concept** : Notation octale où chaque chiffre représente user, group, others.
- 0 = --- (aucune permission)
- 7 = rwx (toutes les permissions)

---

### 9-John_Doe
**Commande** : `chmod 753 hello`

**Description** : Définit les permissions à `-rwxr-x-wx` (753).
- Propriétaire : rwx (7)
- Groupe : r-x (5)
- Autres : -wx (3)

**Concept** : Calcul des permissions octales :
- 7 = 4(r) + 2(w) + 1(x)
- 5 = 4(r) + 0 + 1(x)
- 3 = 0 + 2(w) + 1(x)

---

### 10-mirror_permissions
**Commande** : `chmod --reference=olleh hello`

**Description** : Copie les permissions du fichier `olleh` vers le fichier `hello`.

**Concept** : `--reference` permet de copier les permissions d'un fichier existant.

---

### 11-directories_permissions
**Commande** : `chmod -R a+X .`

**Description** : Ajoute la permission d'exécution à tous les **répertoires** (mais pas aux fichiers) de manière récursive.

**Concept** :
- `-R` = récursif (tous les sous-dossiers)
- `X` (majuscule) = ajoute l'exécution uniquement aux dossiers, pas aux fichiers

---

### 12-directory_permissions
**Commande** : `mkdir -m 751 my_dir`

**Description** : Crée un répertoire avec les permissions 751 (`drwxr-x--x`).

**Concept** : L'option `-m` (mode) permet de définir les permissions lors de la création.

---

### 13-change_group
**Commande** : `chgrp school hello`

**Description** : Change le groupe propriétaire du fichier `hello` en `school`.

**Concept** : `chgrp` (change group) modifie uniquement le groupe, pas le propriétaire.

---

### 14-change_owner_and_group
**Commande** : `chown -R vincent:staff .`

**Description** : Change récursivement le propriétaire en `vincent` et le groupe en `staff` pour tous les fichiers et dossiers du répertoire courant.

**Concept** : Syntaxe `chown utilisateur:groupe` permet de modifier les deux en une commande.

---

### 15-symbolic_link_permissions
**Commande** : `chown -h vincent:staff _hello`

**Description** : Change le propriétaire et le groupe du **lien symbolique** lui-même (pas du fichier cible).

**Concept** : `-h` (no-dereference) modifie le lien, pas la cible du lien.

---

### 16-if_only
**Commande** : `chown --from=guillaume vincent hello`

**Description** : Change le propriétaire du fichier `hello` en `vincent`, uniquement si le propriétaire actuel est `guillaume`.

**Concept** : `--from` permet un changement conditionnel (changement seulement si le propriétaire actuel correspond).

---

## Commandes Clés Apprises

| Commande | Description |
|----------|-------------|
| `su` | Change d'utilisateur (switch user) |
| `whoami` | Affiche l'utilisateur courant |
| `groups` | Affiche les groupes de l'utilisateur |
| `chmod` | Change les permissions d'un fichier |
| `chown` | Change le propriétaire d'un fichier |
| `chgrp` | Change le groupe d'un fichier |
| `touch` | Crée un fichier vide |

---

## Notation des Permissions

### 1. Notation Symbolique

Structure : `[qui][opération][permission]`

**Qui** :
- `u` = user (propriétaire)
- `g` = group (groupe)
- `o` = others (autres)
- `a` = all (tous)

**Opération** :
- `+` = ajouter
- `-` = retirer
- `=` = définir exactement

**Permission** :
- `r` = read (lecture)
- `w` = write (écriture)
- `x` = execute (exécution)
- `X` = exécution (uniquement pour les dossiers)

**Exemples** :
```bash
chmod u+x file       # Ajoute exécution pour le propriétaire
chmod go-w file      # Retire écriture pour groupe et autres
chmod a=r file       # Définit lecture seule pour tout le monde
chmod ug+rw,o-rwx file  # Multiple modifications
```

---

### 2. Notation Octale

Chaque permission a une valeur :
- `r` (read) = 4
- `w` (write) = 2
- `x` (execute) = 1

On additionne pour obtenir un chiffre de 0 à 7 :

| Octal | Binaire | Symbolique | Calcul |
|-------|---------|------------|--------|
| 0 | 000 | --- | 0+0+0 |
| 1 | 001 | --x | 0+0+1 |
| 2 | 010 | -w- | 0+2+0 |
| 3 | 011 | -wx | 0+2+1 |
| 4 | 100 | r-- | 4+0+0 |
| 5 | 101 | r-x | 4+0+1 |
| 6 | 110 | rw- | 4+2+0 |
| 7 | 111 | rwx | 4+2+1 |

**Exemples courants** :
```bash
chmod 644 file   # rw-r--r-- (lecture/écriture pour proprio, lecture pour autres)
chmod 755 file   # rwxr-xr-x (exécution pour tous, écriture proprio seul)
chmod 700 file   # rwx------ (propriétaire uniquement)
chmod 777 file   # rwxrwxrwx (tous les droits pour tous - DANGEREUX !)
```

---

## Options Importantes

- `-R` : Récursif (applique aux sous-dossiers)
- `-h` : Modifie le lien symbolique, pas sa cible
- `--reference=fichier` : Copie les permissions d'un autre fichier
- `--from=ancien_proprio` : Changement conditionnel
- `-m` : Définit les permissions lors de la création (mkdir)

---

## Concepts Clés

### 1. Permissions sur les Répertoires

Pour un **dossier**, les permissions ont un sens différent :
- **r** (read) : Permet de lister le contenu (`ls`)
- **w** (write) : Permet de créer/supprimer des fichiers dans le dossier
- **x** (execute) : Permet d'entrer dans le dossier (`cd`)

**Important** : Pour accéder à un fichier, il faut la permission `x` sur TOUS les dossiers parents.

---

### 2. Permissions Spéciales

Il existe des permissions avancées (non couvertes dans ces exercices) :
- **Setuid** (4000) : Exécute avec les droits du propriétaire
- **Setgid** (2000) : Exécute avec les droits du groupe
- **Sticky bit** (1000) : Seul le propriétaire peut supprimer (ex: `/tmp`)

---

### 3. Bonnes Pratiques de Sécurité

1. **Principe du moindre privilège** : Donnez uniquement les permissions nécessaires
2. **Évitez 777** : Donner tous les droits à tout le monde est dangereux
3. **Fichiers sensibles** : Utilisez 600 (rw-------) pour les fichiers privés
4. **Scripts exécutables** : 755 (rwxr-xr-x) est standard
5. **Vérifiez régulièrement** : Utilisez `ls -l` pour contrôler les permissions

---

## Exemples Pratiques

### Rendre un script exécutable
```bash
chmod +x script.sh
# ou
chmod 755 script.sh
```

### Protéger un fichier privé
```bash
chmod 600 private_key.pem
```

### Permettre au groupe de modifier un fichier
```bash
chmod g+w shared_file.txt
```

### Changer propriétaire et groupe
```bash
chown john:developers project_file.py
```

### Récursif sur un dossier
```bash
chmod -R 755 /var/www/html
chown -R www-data:www-data /var/www/html
```

---

## Commandes de Diagnostic

```bash
ls -l             # Voir les permissions détaillées
ls -ld dossier/   # Voir les permissions d'un dossier
stat fichier      # Informations complètes (permissions octales incluses)
id                # Voir votre UID, GID et groupes
```

---

## Ressources

- `man chmod` : Manuel de chmod
- `man chown` : Manuel de chown
- `man chgrp` : Manuel de chgrp
- [Unix Permissions Calculator](https://chmod-calculator.com/) : Calculateur de permissions
