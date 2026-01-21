# COURS RÉCAPITULATIF - Shell Scripting
## Formation Holberton School - Première Année

---

# TABLE DES MATIÈRES

1. [Introduction au Shell](#introduction-au-shell)
2. [Module 1 : Basics - Les Fondamentaux](#module-1--basics---les-fondamentaux)
3. [Module 2 : Permissions](#module-2--permissions)
4. [Module 3 : I/O Redirections and Filters](#module-3--io-redirections-and-filters)
5. [Module 4 : Init Files, Variables and Expansions](#module-4--init-files-variables-and-expansions)
6. [Synthèse des Compétences Acquises](#synthèse-des-compétences-acquises)
7. [Projet Final et Applications Pratiques](#projet-final-et-applications-pratiques)
8. [Ressources et Aller Plus Loin](#ressources-et-aller-plus-loin)

---

# Introduction au Shell

## Qu'est-ce que le Shell ?

Le **Shell** (coquille en français) est un **interpréteur de commandes** qui sert d'interface entre l'utilisateur et le système d'exploitation Unix/Linux. Il permet de :
- Exécuter des commandes
- Automatiser des tâches
- Manipuler des fichiers et dossiers
- Créer des scripts

## Pourquoi apprendre le Shell ?

1. **Automatisation** : Répéter des tâches automatiquement
2. **Efficacité** : Plus rapide que l'interface graphique pour certaines tâches
3. **Puissance** : Accès complet au système d'exploitation
4. **Serveurs** : Les serveurs Linux n'ont généralement pas d'interface graphique
5. **DevOps** : Compétence essentielle pour l'administration système

## Types de Shell

- **Bash** (Bourne Again Shell) : Le plus courant, celui utilisé dans ce cours
- **Zsh** : Shell moderne avec des fonctionnalités avancées
- **Fish** : Shell convivial pour débutants
- **Sh** : Shell historique original

## Anatomie d'une Commande

```
commande [options] [arguments]
```

**Exemple** :
```bash
ls -la /home
│  │   │
│  │   └─ Argument (sur quoi agir)
│  └─ Option (comment agir)
└─ Commande (que faire)
```

---

# Module 1 : Basics - Les Fondamentaux

## 1.1 - Navigation dans le Système de Fichiers

### Structure du Système de Fichiers Unix

```
/                    (racine - root)
├── bin/            (binaires essentiels)
├── boot/           (fichiers de démarrage)
├── dev/            (périphériques)
├── etc/            (fichiers de configuration)
├── home/           (répertoires utilisateurs)
│   └── user/
│       ├── Documents/
│       ├── Downloads/
│       └── ...
├── tmp/            (fichiers temporaires)
├── usr/            (programmes utilisateur)
│   ├── bin/
│   └── local/
└── var/            (données variables)
    └── log/
```

### Commandes de Navigation

| Commande | Description | Exemple |
|----------|-------------|---------|
| `pwd` | Affiche le répertoire courant | `pwd` → `/home/user` |
| `cd [dir]` | Change de répertoire | `cd Documents` |
| `cd ~` | Va au répertoire personnel | `cd ~` |
| `cd ..` | Remonte d'un niveau | `cd ..` |
| `cd -` | Retourne au répertoire précédent | `cd -` |
| `cd /` | Va à la racine | `cd /` |

### Chemins : Absolus vs Relatifs

**Chemin absolu** : Commence par `/`, part de la racine
```bash
cd /home/user/Documents
```

**Chemin relatif** : Part du répertoire courant
```bash
cd Documents        # Si on est dans /home/user
cd ../Downloads     # Remonte puis descend
```

**Symboles spéciaux** :
- `.` = répertoire courant
- `..` = répertoire parent
- `~` = répertoire personnel (home)
- `-` = répertoire précédent

---

## 1.2 - Lister et Visualiser

### La Commande `ls`

```bash
ls              # Liste basique
ls -l           # Format long (détails)
ls -a           # Affiche les fichiers cachés
ls -la          # Combine -l et -a
ls -lh          # Taille en format humain (KB, MB)
ls -lt          # Trie par date de modification
ls -lS          # Trie par taille
ls -R           # Récursif (sous-dossiers)
```

### Décoder `ls -l`

```
-rwxr-xr-x  1 user group  4096 Jan 21 10:00 script.sh
│││││││││  │  │    │      │    │          └─ Nom
│││││││││  │  │    │      │    └─ Date de modification
│││││││││  │  │    │      └─ Taille (octets)
│││││││││  │  │    └─ Groupe propriétaire
│││││││││  │  └─ Utilisateur propriétaire
│││││││││  └─ Nombre de liens
││││││││└─ Exécution (others)
│││││││└── Écriture (others)
││││││└─── Lecture (others)
│││││└──── Exécution (group)
││││└───── Écriture (group)
│││└────── Lecture (group)
││└─────── Exécution (user)
│└──────── Écriture (user)
└───────── Lecture (user) / Type de fichier
```

**Types de fichiers** :
- `-` : fichier régulier
- `d` : directory (dossier)
- `l` : symbolic link (lien symbolique)
- `c` : character device (périphérique caractère)
- `b` : block device (périphérique bloc)

---

## 1.3 - Manipulation de Fichiers et Dossiers

### Créer

| Commande | Description | Exemple |
|----------|-------------|---------|
| `touch file` | Crée un fichier vide | `touch notes.txt` |
| `mkdir dir` | Crée un dossier | `mkdir project` |
| `mkdir -p path/to/dir` | Crée les dossiers parents | `mkdir -p a/b/c` |

### Copier

```bash
cp source destination          # Copie un fichier
cp -r dossier/ destination/    # Copie un dossier (récursif)
cp -i file dest/               # Demande confirmation si existe
cp -u file dest/               # Copie si plus récent (update)
```

### Déplacer / Renommer

```bash
mv ancien nouveau              # Renomme
mv file dossier/               # Déplace
mv -i file dest/               # Demande confirmation
mv *.txt Documents/            # Déplace tous les .txt
```

### Supprimer

```bash
rm fichier                     # Supprime un fichier
rm -i fichier                  # Demande confirmation
rm -f fichier                  # Force la suppression
rm -r dossier/                 # Supprime récursivement
rm -rf dossier/                # Force récursif (DANGEREUX!)
rmdir dossier/                 # Supprime dossier vide
```

⚠️ **ATTENTION** : Pas de corbeille avec `rm` ! La suppression est définitive.

---

## 1.4 - Liens Symboliques

### Qu'est-ce qu'un Lien Symbolique ?

Un lien symbolique est un **raccourci** vers un autre fichier ou dossier.

```bash
ln -s /chemin/vers/original lien_symbolique
```

**Exemple** :
```bash
ln -s /usr/bin/python3 python
# Maintenant "python" pointe vers /usr/bin/python3
```

**Différence avec un lien dur** :
- **Lien symbolique** : Pointe vers le chemin (si l'original est supprimé, le lien est cassé)
- **Lien dur** : Pointe vers les données (survit à la suppression de l'original)

---

## 1.5 - Wildcards (Jokers)

Les wildcards permettent de sélectionner plusieurs fichiers à la fois.

| Pattern | Signification | Exemple |
|---------|---------------|---------|
| `*` | N'importe quelle chaîne | `*.txt` → tous les fichiers .txt |
| `?` | Un seul caractère | `file?.txt` → file1.txt, fileA.txt |
| `[abc]` | Un caractère parmi a, b, c | `file[123].txt` → file1.txt, file2.txt |
| `[a-z]` | Une lettre minuscule | `[a-z]*.txt` |
| `[^abc]` | Tout sauf a, b, c | `[^0-9]*` → pas de chiffre au début |
| `[[:upper:]]` | Majuscule | `[[:upper:]]*` → commence par majuscule |
| `[[:digit:]]` | Chiffre | `*[[:digit:]].txt` |

**Exemples pratiques** :
```bash
ls *.pdf                    # Tous les PDF
rm file[1-5].txt            # file1.txt à file5.txt
cp *.jpg backup/            # Tous les JPG
mv [A-Z]* uppercase_files/  # Commence par majuscule
```

---

## 1.6 - Détection de Type de Fichier

### La Commande `file`

```bash
file document.pdf
# Sortie: document.pdf: PDF document, version 1.4

file image.jpg
# Sortie: image.jpg: JPEG image data, JFIF standard 1.01

file script.sh
# Sortie: script.sh: Bash script, ASCII text executable
```

**Utilité** : Identifier le type réel d'un fichier indépendamment de son extension.

---

# Module 2 : Permissions

## 2.1 - Le Système de Permissions Unix

### Philosophie de Sécurité

Unix repose sur un modèle de permissions simple mais puissant :
- Chaque fichier/dossier a un **propriétaire** (user)
- Chaque fichier/dossier appartient à un **groupe**
- Les permissions définissent qui peut **lire**, **écrire**, et **exécuter**

### Les Trois Catégories d'Utilisateurs

1. **u (user)** : Le propriétaire du fichier
2. **g (group)** : Les membres du groupe propriétaire
3. **o (others)** : Tous les autres utilisateurs

### Les Trois Types de Permissions

| Permission | Fichier | Dossier | Valeur |
|------------|---------|---------|--------|
| **r** (read) | Lire le contenu | Lister le contenu (`ls`) | 4 |
| **w** (write) | Modifier le fichier | Créer/supprimer fichiers | 2 |
| **x** (execute) | Exécuter le fichier | Entrer dans le dossier (`cd`) | 1 |

---

## 2.2 - Gestion des Utilisateurs et Groupes

### Commandes d'Identification

```bash
whoami              # Affiche votre nom d'utilisateur
id                  # Affiche UID, GID et groupes
groups              # Liste vos groupes
who                 # Affiche les utilisateurs connectés
w                   # Utilisateurs connectés avec détails
```

### Changer d'Utilisateur

```bash
su username         # Switch user (demande mot de passe)
su -                # Devient root avec son environnement
sudo command        # Exécute une commande en tant que root
exit                # Retour à l'utilisateur précédent
```

---

## 2.3 - Modifier les Permissions avec `chmod`

### Notation Symbolique

**Structure** : `chmod [qui][opération][permission] fichier`

```bash
chmod u+x script.sh      # Ajoute exécution pour le propriétaire
chmod g-w file.txt       # Retire écriture pour le groupe
chmod o=r file.txt       # Définit lecture seule pour others
chmod a+x script.sh      # Ajoute exécution pour tous (all)
chmod ug+rw file.txt     # Ajoute lecture+écriture pour user et group
```

**Opérations** :
- `+` : Ajouter
- `-` : Retirer
- `=` : Définir exactement

**Qui** :
- `u` : user
- `g` : group
- `o` : others
- `a` : all (ugo)

---

### Notation Octale

Chaque permission a une valeur numérique :
- `r (read)` = 4
- `w (write)` = 2
- `x (execute)` = 1

On additionne pour obtenir un chiffre de 0 à 7 :

| Octal | Binaire | Symbolique | Calcul | Description |
|-------|---------|------------|--------|-------------|
| 0 | 000 | `---` | 0+0+0 | Aucune permission |
| 1 | 001 | `--x` | 0+0+1 | Exécution seule |
| 2 | 010 | `-w-` | 0+2+0 | Écriture seule |
| 3 | 011 | `-wx` | 0+2+1 | Écriture + Exécution |
| 4 | 100 | `r--` | 4+0+0 | Lecture seule |
| 5 | 101 | `r-x` | 4+0+1 | Lecture + Exécution |
| 6 | 110 | `rw-` | 4+2+0 | Lecture + Écriture |
| 7 | 111 | `rwx` | 4+2+1 | Toutes les permissions |

**Format** : `chmod [user][group][others] fichier`

```bash
chmod 644 file.txt       # rw-r--r-- (propriétaire: rw, autres: r)
chmod 755 script.sh      # rwxr-xr-x (exécutable pour tous)
chmod 700 private.key    # rwx------ (propriétaire uniquement)
chmod 600 secret.txt     # rw------- (lecture/écriture proprio seul)
chmod 777 file.txt       # rwxrwxrwx (DANGEREUX - tout pour tous!)
```

### Permissions Courantes

| Octal | Symbolique | Usage typique |
|-------|------------|---------------|
| 644 | rw-r--r-- | Fichiers publics |
| 600 | rw------- | Fichiers privés (clés SSH) |
| 755 | rwxr-xr-x | Scripts exécutables |
| 700 | rwx------ | Dossiers privés |
| 777 | rwxrwxrwx | À ÉVITER (trop permissif) |

---

### Options Avancées de chmod

```bash
chmod -R 755 dossier/           # Récursif (tous sous-dossiers)
chmod -R a+X dossier/           # +x uniquement pour dossiers (X majuscule)
chmod --reference=ref file      # Copie permissions de "ref" vers "file"
```

---

## 2.4 - Changer le Propriétaire

### `chown` - Change Owner

```bash
chown user fichier              # Change le propriétaire
chown user:group fichier        # Change propriétaire et groupe
chown -R user:group dossier/    # Récursif
chown --from=old new file       # Changement conditionnel
chown -h user lien              # Change le lien, pas la cible
```

**Exemples** :
```bash
chown john document.txt
chown www-data:www-data /var/www/
chown -R alice:developers project/
```

⚠️ **Note** : Nécessite généralement les droits root (`sudo`).

---

### `chgrp` - Change Group

```bash
chgrp group fichier             # Change le groupe
chgrp -R group dossier/         # Récursif
```

**Exemple** :
```bash
chgrp developers project.py
```

---

## 2.5 - Permissions sur les Dossiers

Pour un **dossier**, les permissions ont un sens différent :

| Permission | Signification |
|------------|---------------|
| **r** | Permet de lister le contenu (`ls dossier/`) |
| **w** | Permet de créer/supprimer des fichiers dans le dossier |
| **x** | Permet d'entrer dans le dossier (`cd dossier/`) |

**Important** : Pour accéder à un fichier, il faut la permission **x** sur TOUS les dossiers parents !

**Exemple** :
```bash
# Pour lire /home/user/docs/file.txt, il faut :
# - x sur /home
# - x sur /home/user
# - x sur /home/user/docs
# - r sur /home/user/docs/file.txt
```

---

## 2.6 - Permissions Spéciales

### Setuid (4000)

Permet d'exécuter un fichier avec les droits du propriétaire.

```bash
chmod u+s file
chmod 4755 file
```

**Exemple** : La commande `passwd` a setuid pour modifier `/etc/shadow` en tant que root.

### Setgid (2000)

- **Fichier** : Exécute avec les droits du groupe
- **Dossier** : Les nouveaux fichiers héritent du groupe du dossier

```bash
chmod g+s dossier
chmod 2755 dossier
```

### Sticky Bit (1000)

Sur un dossier : Seul le propriétaire peut supprimer ses propres fichiers.

```bash
chmod +t dossier
chmod 1777 /tmp
```

**Exemple** : `/tmp` a le sticky bit → chacun peut créer des fichiers, mais ne peut supprimer que les siens.

---

## 2.7 - Bonnes Pratiques de Sécurité

1. **Principe du moindre privilège** : Donnez uniquement les permissions nécessaires
2. **Évitez 777** : Trop permissif, risque de sécurité
3. **Fichiers sensibles** : 600 ou 400 pour les clés privées
4. **Scripts exécutables** : 755 (ou 700 si privé)
5. **Dossiers web** : Souvent 755 pour dossiers, 644 pour fichiers
6. **Vérifiez régulièrement** : `find / -perm 777` pour trouver les fichiers trop permissifs

---

# Module 3 : I/O Redirections and Filters

## 3.1 - Les 3 Flux Standard

Chaque processus Unix possède 3 flux :

| Nom | Descripteur | Symbole | Description |
|-----|-------------|---------|-------------|
| **stdin** | 0 | `<` | Entrée standard (clavier par défaut) |
| **stdout** | 1 | `>` | Sortie standard (écran par défaut) |
| **stderr** | 2 | `2>` | Sortie d'erreur (écran par défaut) |

---

## 3.2 - Redirections de Sortie

### Redirection de stdout (`>` et `>>`)

```bash
command > fichier              # Écrase le fichier
command >> fichier             # Ajoute à la fin du fichier
```

**Exemples** :
```bash
ls -la > liste_fichiers.txt    # Sauvegarde le résultat
echo "Nouvelle ligne" >> log.txt
date > date_actuelle.txt
```

---

### Redirection de stderr (`2>`)

```bash
command 2> erreurs.log         # Redirige les erreurs
command 2>> erreurs.log        # Ajoute les erreurs
```

**Exemple** :
```bash
ls dossier_inexistant 2> errors.txt
# Les erreurs vont dans errors.txt
```

---

### Rediriger stdout ET stderr

```bash
command > output.log 2>&1      # Ancienne syntaxe
command &> output.log          # Nouvelle syntaxe (équivalent)
command > /dev/null 2>&1       # Supprime toute sortie
```

**Explication de `2>&1`** :
- `2>` : redirige stderr
- `&1` : vers où pointe stdout

---

### Rediriger vers `/dev/null`

`/dev/null` est un "trou noir" : tout ce qui y est envoyé disparaît.

```bash
command > /dev/null            # Supprime stdout
command 2> /dev/null           # Supprime stderr
command &> /dev/null           # Supprime tout
```

**Utilité** : Ignorer les sorties non désirées.

---

## 3.3 - Redirection d'Entrée (`<`)

```bash
command < fichier              # Lit depuis fichier au lieu du clavier
```

**Exemples** :
```bash
wc -l < file.txt               # Compte les lignes de file.txt
sort < unsorted.txt > sorted.txt
mail -s "Rapport" user@mail.com < rapport.txt
```

---

## 3.4 - Here Documents (`<<`)

Permet de passer plusieurs lignes en entrée :

```bash
command << DELIMITER
ligne 1
ligne 2
ligne 3
DELIMITER
```

**Exemple** :
```bash
cat << EOF > script.sh
#!/bin/bash
echo "Hello World"
EOF
```

---

## 3.5 - Les Pipes (`|`)

Le pipe (`|`) connecte la **sortie** d'une commande à **l'entrée** de la suivante.

```bash
commande1 | commande2 | commande3
```

**Exemples** :
```bash
ls -la | grep ".txt"           # Filtre les fichiers .txt
cat file.txt | sort | uniq     # Trie et supprime doublons
ps aux | grep firefox          # Trouve processus firefox
dmesg | tail -n 20             # 20 dernières lignes du log système
```

---

## 3.6 - Filtres de Texte Essentiels

### `cat` - Concatenate

```bash
cat file.txt                   # Affiche le contenu
cat file1 file2                # Concatène plusieurs fichiers
cat -n file.txt                # Affiche avec numéros de ligne
cat -A file.txt                # Affiche caractères invisibles
```

---

### `head` - Début de Fichier

```bash
head file.txt                  # 10 premières lignes (défaut)
head -n 5 file.txt             # 5 premières lignes
head -c 100 file.txt           # 100 premiers caractères
```

---

### `tail` - Fin de Fichier

```bash
tail file.txt                  # 10 dernières lignes
tail -n 20 file.txt            # 20 dernières lignes
tail -n +5 file.txt            # À partir de la ligne 5
tail -f /var/log/syslog        # Suit le fichier en temps réel
```

**Astuce** : `tail -f` est très utile pour surveiller des logs en direct.

---

### `grep` - Recherche de Patterns

```bash
grep "pattern" file            # Lignes contenant "pattern"
grep -i "pattern" file         # Insensible à la casse
grep -v "pattern" file         # Lignes NE contenant PAS "pattern"
grep -c "pattern" file         # Compte les correspondances
grep -n "pattern" file         # Affiche numéros de ligne
grep -r "pattern" dir/         # Recherche récursive
grep -A 3 "pattern" file       # 3 lignes après le match
grep -B 3 "pattern" file       # 3 lignes avant le match
grep -C 3 "pattern" file       # 3 lignes avant et après
```

**Expressions régulières** :
```bash
grep "^Start" file             # Lignes commençant par "Start"
grep "end$" file               # Lignes finissant par "end"
grep "[0-9]" file              # Lignes contenant un chiffre
grep "^$" file                 # Lignes vides
```

---

### `sort` - Trier

```bash
sort file.txt                  # Tri alphabétique
sort -r file.txt               # Tri inverse
sort -n file.txt               # Tri numérique
sort -u file.txt               # Tri + supprime doublons
sort -k 2 file.txt             # Trie par 2ème colonne
sort -t ',' -k 2 file.csv      # Tri CSV par 2ème colonne
```

---

### `uniq` - Éliminer les Doublons

⚠️ **Important** : `uniq` ne fonctionne que sur des lignes **consécutives** → utilisez `sort` avant !

```bash
sort file.txt | uniq           # Supprime doublons
sort file.txt | uniq -c        # Compte les occurrences
sort file.txt | uniq -d        # Affiche uniquement les doublons
sort file.txt | uniq -u        # Affiche uniquement les lignes uniques
```

---

### `wc` - Word Count

```bash
wc file.txt                    # Lignes, mots, caractères
wc -l file.txt                 # Nombre de lignes uniquement
wc -w file.txt                 # Nombre de mots
wc -c file.txt                 # Nombre d'octets
wc -m file.txt                 # Nombre de caractères
```

---

### `cut` - Découper

```bash
cut -c 1-10 file.txt           # Caractères 1 à 10
cut -f 1,3 file.txt            # Champs 1 et 3 (délimiteur TAB)
cut -d ':' -f 1 /etc/passwd    # 1er champ avec délimiteur ':'
cut -d ',' -f 2-4 data.csv     # Champs 2 à 4 (CSV)
```

---

### `tr` - Translate

```bash
tr 'a' 'z'                     # Remplace 'a' par 'z'
tr 'a-z' 'A-Z'                 # Convertit en majuscules
tr -d 'aeiou'                  # Supprime les voyelles
tr -s ' '                      # Compresse espaces multiples
tr '\n' ','                    # Remplace retours à la ligne par ','
tr -cd '[:digit:]'             # Garde uniquement les chiffres
```

---

### `rev` - Reverse

```bash
rev file.txt                   # Inverse chaque ligne caractère par caractère
```

**Exemple** :
```
Entrée : "Hello World"
Sortie : "dlroW olleH"
```

---

### `sed` - Stream Editor

```bash
sed 's/old/new/' file          # Remplace 1ère occurrence par ligne
sed 's/old/new/g' file         # Remplace toutes occurrences (global)
sed '5d' file                  # Supprime ligne 5
sed '/pattern/d' file          # Supprime lignes contenant pattern
sed -n '10,20p' file           # Affiche lignes 10 à 20
```

---

### `awk` - Pattern Scanning

```bash
awk '{print $1}' file          # Affiche 1ère colonne
awk -F ':' '{print $1}' file   # Délimiteur ':'
awk '{print $1, $3}' file      # Colonnes 1 et 3
awk '$3 > 100' file            # Lignes où colonne 3 > 100
awk 'NR > 1' file              # Ignore 1ère ligne (en-tête)
```

---

## 3.7 - Recherche de Fichiers avec `find`

```bash
find /path -name "*.txt"       # Trouve fichiers .txt
find . -type f                 # Trouve uniquement les fichiers
find . -type d                 # Trouve uniquement les dossiers
find . -name "file*"           # Trouve fichiers commençant par "file"
find . -mtime -7               # Modifiés dans les 7 derniers jours
find . -size +100M             # Plus de 100 MB
find . -empty                  # Fichiers/dossiers vides
find . -perm 777               # Permissions 777
find . -name "*.log" -delete   # Trouve et supprime
find . -name "*.jpg" -exec mv {} dest/ \;  # Exécute commande sur résultats
```

---

## 3.8 - Pipelines Avancés

### Pattern : Filtrer et Compter

```bash
grep "ERROR" log.txt | wc -l
# Compte les lignes d'erreur
```

### Pattern : Trier et Supprimer Doublons

```bash
cat file.txt | sort | uniq
```

### Pattern : Top 10 des Plus Fréquents

```bash
cat file.txt | sort | uniq -c | sort -nr | head -n 10
```

**Explication** :
1. `sort` : trie les lignes
2. `uniq -c` : compte les occurrences
3. `sort -nr` : trie numériquement en ordre décroissant
4. `head -n 10` : garde les 10 premiers

---

### Pattern : Extraire et Traiter une Colonne

```bash
cut -d ',' -f 2 data.csv | sort | uniq
# Extrait 2ème colonne d'un CSV, trie et supprime doublons
```

---

### Pattern : Recherche Complexe

```bash
find /var/log -name "*.log" -exec grep -l "ERROR" {} \;
# Trouve logs contenant "ERROR"
```

---

### Pattern : Statistiques sur Logs

```bash
cat access.log | awk '{print $1}' | sort | uniq -c | sort -nr | head -n 10
# Top 10 des IPs dans un log Apache
```

---

## 3.9 - Chaînes de Traitement Pratiques

### Analyser un fichier CSV

```bash
# Compter les lignes (sans en-tête)
tail -n +2 data.csv | wc -l

# Extraire colonne 3
cut -d ',' -f 3 data.csv

# Valeurs uniques de colonne 2
cut -d ',' -f 2 data.csv | sort | uniq
```

---

### Nettoyer du texte

```bash
# Supprimer lignes vides
grep -v "^$" file.txt

# Supprimer espaces multiples
cat file.txt | tr -s ' '

# Convertir en majuscules
cat file.txt | tr '[:lower:]' '[:upper:]'
```

---

### Surveiller des logs

```bash
# Suivre un log en temps réel
tail -f /var/log/syslog

# Afficher uniquement les erreurs en direct
tail -f /var/log/apache2/error.log | grep "CRITICAL"
```

---

# Module 4 : Init Files, Variables and Expansions

## 4.1 - Variables en Shell

### Types de Variables

1. **Variables locales** : Visibles uniquement dans le shell courant
   ```bash
   MY_VAR="valeur"
   ```

2. **Variables d'environnement** : Transmises aux processus enfants
   ```bash
   export MY_VAR="valeur"
   ```

3. **Variables spéciales** : Définies par le système
   ```bash
   $USER      # Nom d'utilisateur
   $HOME      # Répertoire personnel
   $PATH      # Chemins de recherche
   $PWD       # Répertoire courant
   $SHELL     # Shell par défaut
   $?         # Code de retour dernière commande
   $$         # PID du shell
   $!         # PID du dernier processus en arrière-plan
   ```

---

### Déclarer et Utiliser des Variables

```bash
# Déclaration (pas d'espaces autour de =)
NAME="Alice"
AGE=25

# Utilisation
echo $NAME
echo ${NAME}           # Recommandé (accolades)

# Concaténation
FULL_NAME="${NAME} Smith"

# Valeur par défaut
echo ${VAR:-default}   # Utilise "default" si VAR vide ou non définie
echo ${VAR:=default}   # Définit VAR à "default" si vide
```

---

### Variables d'Environnement

```bash
# Créer une variable d'environnement
export DATABASE_URL="postgres://localhost/db"

# Lister toutes les variables d'environnement
printenv
env

# Lister toutes les variables (locales + environnement)
set

# Supprimer une variable
unset MY_VAR
```

---

## 4.2 - Le PATH

Le `PATH` contient les répertoires où le shell cherche les commandes.

```bash
# Afficher le PATH
echo $PATH
# Sortie: /usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin

# Ajouter un répertoire au PATH (temporaire)
export PATH="$PATH:/mon/nouveau/repertoire"

# Ajouter au début (prioritaire)
export PATH="/mon/nouveau/repertoire:$PATH"

# Ajouter de façon permanente (dans ~/.bashrc)
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.bashrc
```

**Ordre de recherche** : Le shell cherche de gauche à droite dans le PATH.

---

## 4.3 - Alias

Les alias créent des raccourcis pour des commandes.

```bash
# Créer un alias (temporaire)
alias ll='ls -la'
alias gs='git status'
alias ..='cd ..'

# Lister tous les alias
alias

# Supprimer un alias
unalias ll

# Ignorer un alias (exécuter la commande originale)
\ls
```

### Alias Permanents

Ajoutez vos alias dans `~/.bashrc` ou `~/.bash_aliases` :

```bash
# Navigation
alias ..='cd ..'
alias ...='cd ../..'
alias home='cd ~'

# Commandes avec couleurs
alias ls='ls --color=auto'
alias grep='grep --color=auto'

# Raccourcis
alias ll='ls -lah'
alias la='ls -A'

# Git
alias gs='git status'
alias ga='git add'
alias gc='git commit'
alias gp='git push'
alias gl='git log --oneline'

# Sécurité
alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'

# Utilitaires
alias h='history'
alias c='clear'
alias path='echo $PATH | tr ":" "\n"'
```

---

## 4.4 - Expansions

### 1. Expansion de Variables

```bash
NAME="Alice"
echo $NAME              # Alice
echo ${NAME}            # Alice (recommandé)
echo "Hello $NAME"      # Hello Alice
echo 'Hello $NAME'      # Hello $NAME (pas d'expansion avec ')
```

### 2. Expansion de Commande

```bash
# Syntaxe moderne (recommandée)
TODAY=$(date +%Y-%m-%d)
FILES=$(ls | wc -l)

# Ancienne syntaxe (backticks)
TODAY=`date +%Y-%m-%d`

# Dans une chaîne
echo "Aujourd'hui : $(date)"
```

### 3. Expansion Arithmétique

```bash
# Syntaxe : $(( expression ))
echo $((2 + 3))         # 5
echo $((10 * 5))        # 50
echo $((10 / 3))        # 3 (division entière)
echo $((10 % 3))        # 1 (modulo)
echo $((2 ** 8))        # 256 (puissance)

# Avec variables
A=10
B=5
echo $((A + B))         # 15

# Incrément
((i++))
((i += 5))

# Dans une variable
RESULT=$((5 * 10))
```

**Opérateurs arithmétiques** :
- `+` : addition
- `-` : soustraction
- `*` : multiplication
- `/` : division entière
- `%` : modulo (reste)
- `**` : puissance
- `++` : incrément
- `--` : décrément

---

### 4. Expansion d'Accolades

```bash
# Séquences
echo {1..10}            # 1 2 3 4 5 6 7 8 9 10
echo {a..z}             # a b c ... z
echo {01..10}           # 01 02 03 ... 10
echo {10..1}            # 10 9 8 ... 1
echo {a..z..2}          # a c e g ... (pas de 2)

# Listes
echo {red,green,blue}   # red green blue

# Combinaisons
echo file{1..3}.txt     # file1.txt file2.txt file3.txt
echo {A,B}{1,2}         # A1 A2 B1 B2

# Créer des fichiers
touch file{1..10}.txt   # Crée file1.txt à file10.txt

# Créer une arborescence
mkdir -p project/{src,docs,tests}/{js,css,html}
```

---

### 5. Expansion de Tilde

```bash
~               # /home/username
~/Documents     # /home/username/Documents
~user           # /home/user (home d'un autre utilisateur)
~+              # $PWD (répertoire courant)
~-              # $OLDPWD (répertoire précédent)
```

---

## 4.5 - Formatage avec `printf`

`printf` offre un formatage plus avancé que `echo`.

```bash
# Syntaxe : printf "format" arguments

# Chaînes
printf "Hello %s\n" "World"         # Hello World

# Entiers
printf "Nombre: %d\n" 42            # Nombre: 42

# Flottants
printf "Pi: %.2f\n" 3.14159         # Pi: 3.14

# Hexadécimal
printf "Hex: %x\n" 255              # Hex: ff

# Octal
printf "Octal: %o\n" 8              # Octal: 10

# Largeur fixe
printf "%10s | %5d\n" "Name" 123    # "      Name |   123"

# Remplissage avec zéros
printf "%05d\n" 42                  # 00042
```

**Format specifiers** :
- `%s` : string
- `%d` : decimal integer
- `%f` : floating point
- `%x` : hexadecimal (minuscules)
- `%X` : hexadecimal (majuscules)
- `%o` : octal
- `%%` : caractère `%` littéral

---

## 4.6 - Conversions de Bases

### Déclaration en Différentes Bases

```bash
# Bash supporte : base#nombre
echo $((2#1010))        # Binaire → 10
echo $((8#17))          # Octal → 15
echo $((16#FF))         # Hexadécimal → 255
```

### Tableau de Conversion

| Décimal | Binaire | Octal | Hexadécimal |
|---------|---------|-------|-------------|
| 0 | 0 | 0 | 0 |
| 1 | 1 | 1 | 1 |
| 8 | 1000 | 10 | 8 |
| 10 | 1010 | 12 | A |
| 15 | 1111 | 17 | F |
| 16 | 10000 | 20 | 10 |
| 255 | 11111111 | 377 | FF |

### Conversions avec printf

```bash
# Décimal → Hexadécimal
printf "%x\n" 255               # ff

# Décimal → Octal
printf "%o\n" 15                # 17

# Avec majuscules
printf "%X\n" 255               # FF
```

### Binaire avec bc

```bash
# Décimal → Binaire
echo "obase=2; 10" | bc         # 1010

# Binaire → Décimal
echo "ibase=2; 1010" | bc       # 10

# Hexadécimal → Décimal
echo "ibase=16; FF" | bc        # 255
```

---

## 4.7 - Fichiers d'Initialisation

### Bash Startup Files

Quand vous ouvrez un terminal, Bash lit des fichiers de configuration :

| Fichier | Type | Quand chargé |
|---------|------|--------------|
| `/etc/profile` | Système | Login shell (tous users) |
| `/etc/bash.bashrc` | Système | Shell interactif (tous users) |
| `~/.bash_profile` | Utilisateur | Login shell |
| `~/.bash_login` | Utilisateur | Login shell (si pas .bash_profile) |
| `~/.profile` | Utilisateur | Login shell (si pas les 2 autres) |
| `~/.bashrc` | Utilisateur | Shell interactif non-login |
| `~/.bash_logout` | Utilisateur | À la déconnexion |

**Login shell** : Connexion SSH, terminal graphique initial
**Non-login shell** : Nouveau terminal dans une session existante

---

### Bonne Pratique : ~/.bashrc

Mettez vos configurations dans `~/.bashrc` et sourcez-le depuis `~/.bash_profile` :

```bash
# Dans ~/.bash_profile
if [ -f ~/.bashrc ]; then
    source ~/.bashrc
fi
```

### Exemple de ~/.bashrc

```bash
# Alias
alias ll='ls -lah'
alias gs='git status'
alias ..='cd ..'

# Variables d'environnement
export EDITOR=vim
export VISUAL=vim

# PATH personnalisé
export PATH="$HOME/bin:$HOME/.local/bin:$PATH"

# Prompt personnalisé (PS1)
export PS1="\[\e[32m\]\u@\h:\[\e[34m\]\w\[\e[0m\]\$ "

# Historique
export HISTSIZE=10000
export HISTFILESIZE=20000

# Fonctions personnalisées
mkcd() {
    mkdir -p "$1" && cd "$1"
}
```

### Recharger la Configuration

```bash
source ~/.bashrc
# ou
. ~/.bashrc
```

---

## 4.8 - ROT13

ROT13 est un chiffrement par substitution simple : chaque lettre est remplacée par la lettre 13 positions après dans l'alphabet.

```
A → N    N → A
B → O    O → B
...
M → Z    Z → M
```

**Particularité** : Appliquer ROT13 deux fois redonne le texte original.

```bash
echo "Hello" | tr 'A-Za-z' 'N-ZA-Mn-za-m'
# Sortie : Uryyb

echo "Uryyb" | tr 'A-Za-z' 'N-ZA-Mn-za-m'
# Sortie : Hello
```

---

# Synthèse des Compétences Acquises

## Compétences Techniques

### 1. Navigation et Gestion de Fichiers
- Naviguer efficacement dans le système de fichiers Unix
- Créer, copier, déplacer, supprimer fichiers et dossiers
- Utiliser les wildcards pour manipuler plusieurs fichiers
- Créer et gérer des liens symboliques

### 2. Permissions et Sécurité
- Comprendre le modèle de permissions Unix (user/group/others)
- Modifier les permissions en notation symbolique et octale
- Changer propriétaires et groupes
- Appliquer le principe du moindre privilège

### 3. Traitement de Texte et Données
- Utiliser les redirections (stdin, stdout, stderr)
- Maîtriser les pipes pour créer des pipelines complexes
- Filtrer et transformer du texte avec grep, sed, awk, cut, tr
- Trier, compter, et analyser des données

### 4. Programmation Shell
- Créer et utiliser des variables (locales et d'environnement)
- Effectuer des calculs avec l'arithmétique shell
- Utiliser les expansions (variables, commandes, accolades)
- Créer des alias pour automatiser des tâches
- Configurer son environnement shell

### 5. Recherche et Filtrage
- Rechercher des fichiers avec find
- Filtrer du texte avec grep et expressions régulières
- Analyser des logs et extraire des informations

---

## Compétences Transversales

1. **Pensée logique** : Décomposer un problème en étapes simples
2. **Automatisation** : Identifier et automatiser les tâches répétitives
3. **Débogage** : Lire et interpréter les messages d'erreur
4. **Documentation** : Utiliser les pages man et la documentation
5. **Efficacité** : Choisir les bons outils pour chaque tâche

---

# Projet Final et Applications Pratiques

## Projets Suggérés

### 1. Script de Sauvegarde Automatique

```bash
#!/bin/bash
# backup.sh - Sauvegarde automatique avec date

BACKUP_DIR="$HOME/backups"
DATE=$(date +%Y%m%d_%H%M%S)
SOURCE_DIR="$HOME/Documents/important"

mkdir -p "$BACKUP_DIR"
tar -czf "$BACKUP_DIR/backup_$DATE.tar.gz" "$SOURCE_DIR"

echo "Sauvegarde créée : backup_$DATE.tar.gz"

# Supprimer les sauvegardes de plus de 30 jours
find "$BACKUP_DIR" -name "backup_*.tar.gz" -mtime +30 -delete
```

---

### 2. Analyseur de Logs

```bash
#!/bin/bash
# log_analyzer.sh - Analyse un fichier de log

LOG_FILE="/var/log/apache2/access.log"

echo "=== Top 10 des IPs ==="
cat "$LOG_FILE" | awk '{print $1}' | sort | uniq -c | sort -nr | head -n 10

echo ""
echo "=== URLs les plus visitées ==="
cat "$LOG_FILE" | awk '{print $7}' | sort | uniq -c | sort -nr | head -n 10

echo ""
echo "=== Codes de statut HTTP ==="
cat "$LOG_FILE" | awk '{print $9}' | sort | uniq -c | sort -nr
```

---

### 3. Gestionnaire de Projet

```bash
#!/bin/bash
# new_project.sh - Crée structure de projet

PROJECT_NAME=$1

if [ -z "$PROJECT_NAME" ]; then
    echo "Usage: $0 <nom_du_projet>"
    exit 1
fi

mkdir -p "$PROJECT_NAME"/{src,docs,tests,config}
touch "$PROJECT_NAME"/README.md
touch "$PROJECT_NAME"/src/main.sh
chmod +x "$PROJECT_NAME"/src/main.sh

echo "# $PROJECT_NAME" > "$PROJECT_NAME"/README.md
echo "#!/bin/bash" > "$PROJECT_NAME"/src/main.sh

echo "Projet $PROJECT_NAME créé avec succès !"
tree "$PROJECT_NAME"
```

---

### 4. Nettoyeur de Système

```bash
#!/bin/bash
# cleanup.sh - Nettoie fichiers temporaires

echo "Nettoyage en cours..."

# Vider la corbeille
rm -rf ~/.local/share/Trash/*

# Supprimer fichiers temporaires
find /tmp -type f -mtime +7 -delete

# Supprimer fichiers de sauvegarde Emacs
find ~ -name "*~" -delete

# Supprimer caches
rm -rf ~/.cache/thumbnails/*

echo "Nettoyage terminé !"
```

---

### 5. Moniteur de Disque

```bash
#!/bin/bash
# disk_monitor.sh - Alerte si disque plein

THRESHOLD=80

USAGE=$(df / | tail -n 1 | awk '{print $5}' | sed 's/%//')

if [ "$USAGE" -gt "$THRESHOLD" ]; then
    echo "ALERTE : Disque à ${USAGE}% d'utilisation !"
    df -h /
else
    echo "Utilisation disque : ${USAGE}% (OK)"
fi
```

---

## Cas d'Usage Professionnels

### DevOps et Administration Système
- Automatiser le déploiement d'applications
- Gérer les configurations de serveurs
- Surveiller les ressources système
- Créer des scripts de maintenance

### Développement Web
- Automatiser les builds et tests
- Gérer les environnements (dev/staging/prod)
- Analyser les logs d'accès
- Compresser et optimiser les assets

### Data Science
- Prétraiter des fichiers CSV/JSON
- Nettoyer des données
- Automatiser des pipelines de données
- Générer des rapports

### Sécurité
- Analyser des logs de sécurité
- Auditer les permissions de fichiers
- Rechercher des vulnérabilités
- Automatiser des scans

---

# Ressources et Aller Plus Loin

## Documentation Essentielle

### Pages Man (Manuel)
```bash
man bash        # Manuel de Bash
man ls          # Manuel de ls
man chmod       # Manuel de chmod
man grep        # Manuel de grep

# Navigation dans man :
# Espace : page suivante
# b : page précédente
# /pattern : recherche
# n : occurrence suivante
# q : quitter
```

### Commande `help`
```bash
help cd         # Aide sur les commandes intégrées
help export
help alias
```

### Option `--help`
```bash
ls --help
grep --help
find --help
```

---

## Outils en Ligne

### Testeurs et Explainers
- [ExplainShell](https://explainshell.com/) : Explication visuelle des commandes
- [ShellCheck](https://www.shellcheck.net/) : Analyse statique de scripts
- [Regex101](https://regex101.com/) : Testeur d'expressions régulières
- [Chmod Calculator](https://chmod-calculator.com/) : Calculateur de permissions

---

## Livres et Guides

### Débutants
- **"The Linux Command Line"** par William Shotts (gratuit en ligne)
- **Bash Guide for Beginners** (TLDP)

### Intermédiaire
- **"Learning the Bash Shell"** par Cameron Newham
- **Advanced Bash-Scripting Guide** (TLDP)

### Avancé
- **"Classic Shell Scripting"** par Arnold Robbins
- **"Bash Cookbook"** par Carl Albing

---

## Cours en Ligne

- [Linux Journey](https://linuxjourney.com/) : Tutoriels interactifs gratuits
- [Bash Academy](https://www.bash.academy/) : Cours complet sur Bash
- [OverTheWire: Bandit](https://overthewire.org/wargames/bandit/) : Jeu pour apprendre le Shell
- [Codecademy: Learn the Command Line](https://www.codecademy.com/learn/learn-the-command-line)

---

## Communautés

- **Stack Overflow** : Tag `bash`, `shell`, `linux`
- **Unix & Linux Stack Exchange** : Questions spécialisées
- **Reddit** : r/bash, r/linux, r/commandline
- **IRC** : #bash sur Libera.Chat

---

## Prochaines Étapes

### 1. Scripting Avancé
- Structures de contrôle (if, for, while, case)
- Fonctions et modules
- Gestion des erreurs (trap, set -e)
- Débogage (set -x, bash -x)

### 2. Outils Avancés
- `awk` : Langage complet de traitement de texte
- `sed` : Éditeur de flux puissant
- `regex` : Maîtriser les expressions régulières
- `xargs` : Construire et exécuter des commandes

### 3. Administration Système
- Gestion des processus (ps, top, kill)
- Gestion des services (systemd)
- Cron jobs et automatisation
- Monitoring et logs

### 4. Outils Modernes
- **ripgrep** (rg) : Alternative moderne à grep
- **fd** : Alternative à find
- **bat** : Alternative à cat avec coloration
- **exa** : Alternative à ls avec couleurs
- **zsh** : Shell moderne avec plugins (Oh My Zsh)

---

## Mini-Défis pour S'entraîner

### Niveau Débutant
1. Créer un script qui affiche "Bonjour [nom]" avec le nom en argument
2. Lister tous les fichiers .txt d'un dossier et les copier dans un dossier backup
3. Créer 100 fichiers nommés file001.txt à file100.txt

### Niveau Intermédiaire
4. Script qui compte les occurrences de chaque mot dans un fichier
5. Analyser un fichier CSV et afficher la moyenne d'une colonne
6. Créer un script de renommage de masse (ex: ajouter un préfixe à tous les fichiers)

### Niveau Avancé
7. Script qui surveille l'utilisation CPU et envoie une alerte si > 80%
8. Parser un fichier JSON et extraire des données spécifiques
9. Créer un gestionnaire de versions simple (comme Git, mais basique)
10. Script interactif avec menu pour gérer des tâches

---

## Commandes à Connaître Absolument

### Top 20 des Commandes Essentielles

1. `cd` - Change directory
2. `ls` - List files
3. `pwd` - Print working directory
4. `cat` - Concatenate and display files
5. `grep` - Search patterns
6. `find` - Search files
7. `chmod` - Change permissions
8. `chown` - Change owner
9. `cp` - Copy
10. `mv` - Move/rename
11. `rm` - Remove
12. `mkdir` - Make directory
13. `touch` - Create empty file
14. `echo` - Print text
15. `head` / `tail` - View file beginning/end
16. `sort` - Sort lines
17. `uniq` - Remove duplicates
18. `wc` - Word count
19. `sed` - Stream editor
20. `awk` - Pattern scanning

---

## Raccourcis Clavier Essentiels

| Raccourci | Action |
|-----------|--------|
| **Ctrl + C** | Interrompt la commande en cours |
| **Ctrl + D** | EOF (fin de fichier) / Déconnexion |
| **Ctrl + L** | Efface l'écran (comme `clear`) |
| **Ctrl + A** | Début de ligne |
| **Ctrl + E** | Fin de ligne |
| **Ctrl + U** | Efface jusqu'au début de ligne |
| **Ctrl + K** | Efface jusqu'à la fin de ligne |
| **Ctrl + W** | Efface le mot précédent |
| **Ctrl + R** | Recherche dans l'historique |
| **Tab** | Autocomplétion |
| **↑** / **↓** | Parcourir l'historique |

---

## Philosophie Unix

Le Shell Bash s'inscrit dans la philosophie Unix :

1. **Faire une chose et bien la faire** : Chaque commande a un rôle précis
2. **Travailler ensemble** : Les commandes peuvent être combinées (pipes)
3. **Utiliser du texte** : Format universel d'échange de données
4. **Tout est fichier** : Périphériques, processus, tout est accessible comme un fichier

---

# Conclusion

Félicitations ! Tu as maintenant une base solide en Shell scripting. Tu maîtrises :

- La **navigation** et la **gestion de fichiers**
- Le système de **permissions Unix**
- Les **redirections** et **pipes**
- Les **variables** et **expansions**
- Le **traitement de texte** avancé

## Conseils pour Progresser

1. **Pratique quotidienne** : Utilise le terminal pour tes tâches quotidiennes
2. **Lis du code** : Étudie des scripts existants pour apprendre de nouvelles techniques
3. **Automatise** : Dès qu'une tâche se répète, crée un script
4. **Documente** : Commente tes scripts pour les comprendre plus tard
5. **Partage** : Contribue à des projets open source

## Le Shell est un Superpower

Maîtriser le Shell te rend **10x plus productif**. Tu peux maintenant :
- Automatiser n'importe quelle tâche répétitive
- Analyser des données volumineuses en quelques secondes
- Administrer des serveurs Linux efficacement
- Créer des outils personnalisés adaptés à tes besoins

**Continue à apprendre, à expérimenter, et à créer !**

---

*Document créé dans le cadre de la formation Holberton School*
*Tous les scripts et exercices sont disponibles dans ce repository*

**Happy Scripting! 🚀**
