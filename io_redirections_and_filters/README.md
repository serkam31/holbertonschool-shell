# Shell I/O Redirections and Filters

Ce dossier contient 27 scripts qui couvrent les redirections d'entrée/sortie, les pipes, et le traitement de texte avec les filtres Unix.

## Objectifs d'apprentissage

- Maîtriser les redirections d'entrée/sortie (`>`, `>>`, `<`, `2>`)
- Utiliser les pipes (`|`) pour chaîner des commandes
- Manipuler du texte avec les filtres Unix classiques
- Créer des pipelines complexes de traitement de données

---

## Concepts Fondamentaux

### Les 3 Flux Standard

Chaque programme Unix possède 3 flux :
- **stdin (0)** : Entrée standard (clavier par défaut)
- **stdout (1)** : Sortie standard (écran par défaut)
- **stderr (2)** : Sortie d'erreur (écran par défaut)

### Opérateurs de Redirection

| Opérateur | Description | Exemple |
|-----------|-------------|---------|
| `>` | Redirige stdout vers un fichier (écrase) | `ls > files.txt` |
| `>>` | Redirige stdout vers un fichier (ajoute) | `echo "new" >> log.txt` |
| `<` | Redirige un fichier vers stdin | `wc -l < file.txt` |
| `2>` | Redirige stderr vers un fichier | `ls error 2> errors.log` |
| `2>&1` | Redirige stderr vers stdout | `cmd > out.txt 2>&1` |
| `&>` | Redirige stdout et stderr | `cmd &> all.log` |
| `\|` | Pipe : stdout de cmd1 → stdin de cmd2 | `ls \| grep txt` |

---

## Liste des Scripts

### 0-hello_world
**Commande** : `echo "Hello, World"`

**Description** : Affiche "Hello, World" suivi d'une nouvelle ligne.

**Concept** : `echo` affiche du texte sur la sortie standard.

---

### 1-confused_smiley
**Commande** : `echo "\"(Ôo)'"`

**Description** : Affiche un smiley confus avec des caractères spéciaux.

**Concept** : Échappement des caractères spéciaux avec `\` et utilisation de guillemets.

---

### 2-hellofile
**Commande** : `cat /etc/passwd`

**Description** : Affiche le contenu du fichier `/etc/passwd`.

**Concept** : `cat` (concatenate) lit et affiche le contenu d'un ou plusieurs fichiers.

---

### 3-twofiles
**Commande** : `cat /etc/passwd /etc/hosts`

**Description** : Affiche le contenu de deux fichiers successivement.

**Concept** : `cat` peut prendre plusieurs fichiers en arguments.

---

### 4-lastlines
**Commande** : `tail /etc/passwd`

**Description** : Affiche les 10 dernières lignes de `/etc/passwd`.

**Concept** : `tail` affiche la fin d'un fichier (par défaut 10 lignes).

---

### 5-firstlines
**Commande** : `head /etc/passwd`

**Description** : Affiche les 10 premières lignes de `/etc/passwd`.

**Concept** : `head` affiche le début d'un fichier (par défaut 10 lignes).

---

### 6-third_line
**Commande** : `head -n 3 iacta | tail -n 1`

**Description** : Affiche uniquement la 3ème ligne du fichier `iacta`.

**Concept** : Combinaison de pipes pour extraire une ligne précise.
- `head -n 3` : garde les 3 premières lignes
- `tail -n 1` : garde la dernière ligne du résultat

---

### 7-file
**Commande** : `echo "Best School" > \*\\'"Best School"\'\\*$\?\*\*\*\*\*:)`

**Description** : Crée un fichier avec un nom contenant des caractères spéciaux et y écrit "Best School".

**Concept** : Échappement de caractères spéciaux pour créer des noms de fichiers complexes.

---

### 8-cwd_state
**Commande** : `ls -la > ls_cwd_content`

**Description** : Redirige le résultat de `ls -la` vers le fichier `ls_cwd_content`.

**Concept** : Redirection de sortie avec `>` pour sauvegarder le résultat dans un fichier.

---

### 9-duplicate_last_line
**Commande** : `tail -n 1 iacta >> iacta`

**Description** : Duplique la dernière ligne du fichier `iacta` et l'ajoute à la fin du même fichier.

**Concept** : `>>` ajoute à la fin du fichier au lieu d'écraser.

---

### 10-no_more_js
**Commande** : `find . -type f -name "*.js" -delete`

**Description** : Supprime tous les fichiers `.js` du répertoire courant et de ses sous-répertoires.

**Concept** :
- `find` recherche des fichiers selon des critères
- `-type f` : uniquement les fichiers
- `-name "*.js"` : nom se terminant par `.js`
- `-delete` : supprime les fichiers trouvés

---

### 11-directories
**Commande** : `find . -type d -not -path . | wc -l`

**Description** : Compte le nombre de répertoires (et sous-répertoires) dans le dossier courant.

**Concept** :
- `find . -type d` : trouve tous les dossiers
- `-not -path .` : exclut le dossier courant lui-même
- `wc -l` : compte les lignes

---

### 12-newest_files
**Commande** : `ls -t | head -n 10`

**Description** : Affiche les 10 fichiers les plus récents du répertoire courant.

**Concept** :
- `ls -t` : trie par date de modification (les plus récents en premier)
- `head -n 10` : garde les 10 premiers

---

### 13-unique
**Commande** : `sort | uniq -u`

**Description** : Affiche uniquement les lignes qui apparaissent une seule fois (lignes uniques).

**Concept** :
- `sort` : trie les lignes (nécessaire pour uniq)
- `uniq -u` : affiche uniquement les lignes uniques (non répétées)

---

### 14-findthatword
**Commande** : `grep "root" /etc/passwd`

**Description** : Affiche toutes les lignes contenant le mot "root" dans `/etc/passwd`.

**Concept** : `grep` recherche des patterns dans du texte.

---

### 15-countthatword
**Commande** : `grep -c "bin" /etc/passwd`

**Description** : Compte le nombre de lignes contenant "bin" dans `/etc/passwd`.

**Concept** : `grep -c` compte les lignes correspondantes au lieu de les afficher.

---

### 16-whatsnext
**Commande** : `grep -A 3 "root" /etc/passwd`

**Description** : Affiche les lignes contenant "root" plus les 3 lignes suivantes.

**Concept** : `grep -A N` (After) affiche N lignes de contexte après chaque match.

---

### 17-hidethisword
**Commande** : `grep -v "bin" /etc/passwd`

**Description** : Affiche toutes les lignes ne contenant PAS "bin".

**Concept** : `grep -v` (invert) inverse la recherche (affiche les non-correspondances).

---

### 18-letteronly
**Commande** : `grep "^[[:alpha:]]" /etc/ssh/sshd_config`

**Description** : Affiche uniquement les lignes commençant par une lettre.

**Concept** :
- `^` : début de ligne (regex)
- `[[:alpha:]]` : classe de caractères POSIX pour les lettres

---

### 19-AZ
**Commande** : `tr 'Ac' 'Ze'`

**Description** : Remplace tous les 'A' par 'Z' et tous les 'c' par 'e'.

**Concept** : `tr` (translate) remplace des caractères par d'autres.

---

### 20-hiago
**Commande** : `tr -d 'cC'`

**Description** : Supprime tous les caractères 'c' et 'C' de l'entrée.

**Concept** : `tr -d` (delete) supprime les caractères spécifiés.

---

### 21-reverse
**Commande** : `rev`

**Description** : Inverse l'ordre des caractères sur chaque ligne.

**Concept** : `rev` reverse chaque ligne caractère par caractère.

**Exemple** :
```
Entrée : "Hello"
Sortie : "olleH"
```

---

### 22-users_and_homes
**Commande** : `cut -d ':' -f 1,6 /etc/passwd | sort`

**Description** : Affiche les utilisateurs et leur répertoire home depuis `/etc/passwd`, triés alphabétiquement.

**Concept** :
- `cut -d ':' -f 1,6` : découpe avec délimiteur `:`, garde champs 1 et 6
- `sort` : trie alphabétiquement

---

### 23-empty_casks
**Commande** : `find . -empty -printf "%f\n" | sort`

**Description** : Trouve tous les fichiers et dossiers vides, affiche seulement leur nom.

**Concept** :
- `find . -empty` : trouve les fichiers/dossiers vides
- `-printf "%f\n"` : affiche seulement le nom du fichier

---

### 24-gifs
**Commande** : `find . -type f -name "*.gif" -printf "%f\n" | rev | cut -d '.' -f 2- | rev | sort -f`

**Description** : Liste tous les fichiers `.gif`, affiche leur nom sans extension, triés par ordre alphabétique (insensible à la casse).

**Concept** : Pipeline complexe :
1. Trouve les fichiers .gif
2. Affiche le nom uniquement
3. Inverse la chaîne
4. Coupe l'extension
5. Inverse à nouveau
6. Trie (insensible à la casse)

---

### 25-acrostic
**Commande** : `cut -c 1 | tr -d '\n' | sort`

**Description** : Affiche le premier caractère de chaque ligne pour former un acrostiche.

**Concept** :
- `cut -c 1` : coupe le premier caractère
- `tr -d '\n'` : supprime les retours à la ligne

---

### 26-the_biggest_fan
**Commande** : `tail -n +2 | cut -f 1 | sort | uniq -c | sort -nr | head -n 11 | tr -s ' ' | cut -d ' ' -f 3`

**Description** : Parse un fichier de logs pour afficher les 10 IPs les plus actives.

**Concept** : Pipeline avancé de traitement de données :
1. `tail -n +2` : ignore la première ligne (en-tête)
2. `cut -f 1` : extrait le premier champ
3. `sort` : trie
4. `uniq -c` : compte les occurrences
5. `sort -nr` : trie numériquement en ordre décroissant
6. `head -n 11` : garde les 11 premiers
7. `tr -s ' '` : compresse les espaces multiples
8. `cut -d ' ' -f 3` : extrait le 3ème champ (l'IP)

---

## Commandes Clés Apprises

| Commande | Description |
|----------|-------------|
| `cat` | Affiche le contenu de fichiers |
| `head` | Affiche le début d'un fichier |
| `tail` | Affiche la fin d'un fichier |
| `echo` | Affiche du texte |
| `grep` | Recherche des patterns dans du texte |
| `sort` | Trie des lignes |
| `uniq` | Filtre les lignes dupliquées |
| `cut` | Découpe des lignes en champs |
| `tr` | Traduit ou supprime des caractères |
| `rev` | Inverse les caractères d'une ligne |
| `wc` | Compte lignes/mots/caractères |
| `find` | Recherche des fichiers |

---

## Options Importantes

### grep
- `-v` : Inverse (lignes ne correspondant PAS)
- `-c` : Compte les lignes correspondantes
- `-i` : Insensible à la casse
- `-A N` : Affiche N lignes après le match
- `-B N` : Affiche N lignes avant le match
- `-C N` : Affiche N lignes avant et après

### sort
- `-r` : Ordre inverse (décroissant)
- `-n` : Tri numérique
- `-f` : Insensible à la casse
- `-t` : Spécifie le délimiteur

### uniq
- `-c` : Compte les occurrences
- `-u` : Uniquement les lignes uniques
- `-d` : Uniquement les lignes dupliquées

### cut
- `-d` : Spécifie le délimiteur
- `-f` : Sélectionne les champs
- `-c` : Sélectionne les caractères

### tail / head
- `-n N` : Affiche N lignes
- `-n +N` : (tail) Affiche à partir de la ligne N

### tr
- `-d` : Supprime des caractères
- `-s` : Compresse les caractères répétés

### find
- `-type f` : Uniquement les fichiers
- `-type d` : Uniquement les dossiers
- `-name` : Recherche par nom
- `-empty` : Trouve les fichiers/dossiers vides
- `-delete` : Supprime les résultats

---

## Concepts Clés

### 1. Pipes (`|`)

Les pipes permettent de chaîner des commandes :
```bash
commande1 | commande2 | commande3
```

La sortie de commande1 devient l'entrée de commande2, etc.

**Exemple** :
```bash
cat file.txt | grep "error" | sort | uniq
```

---

### 2. Redirections

```bash
# Écraser un fichier
echo "text" > file.txt

# Ajouter à un fichier
echo "more" >> file.txt

# Rediriger stdin depuis un fichier
wc -l < file.txt

# Rediriger stderr
ls nonexistent 2> errors.log

# Rediriger stdout et stderr
command &> all_output.log

# Rediriger stderr vers stdout
command 2>&1

# Rediriger stdout vers stderr
echo "error" >&2
```

---

### 3. Expressions Régulières (Regex) Basiques

| Pattern | Signification |
|---------|---------------|
| `^` | Début de ligne |
| `$` | Fin de ligne |
| `.` | N'importe quel caractère |
| `*` | 0 ou plus occurrences |
| `[abc]` | Un caractère parmi a, b, ou c |
| `[^abc]` | N'importe quel caractère sauf a, b, ou c |
| `[a-z]` | N'importe quelle lettre minuscule |
| `[[:alpha:]]` | N'importe quelle lettre |
| `[[:digit:]]` | N'importe quel chiffre |

---

### 4. Classes de Caractères POSIX

- `[[:alpha:]]` : Lettres
- `[[:digit:]]` : Chiffres
- `[[:alnum:]]` : Lettres et chiffres
- `[[:space:]]` : Espaces blancs
- `[[:upper:]]` : Majuscules
- `[[:lower:]]` : Minuscules

---

## Patterns de Pipelines Courants

### Compter des lignes
```bash
grep "pattern" file | wc -l
```

### Top 10 des plus fréquents
```bash
sort file | uniq -c | sort -nr | head -n 10
```

### Supprimer les doublons
```bash
sort file | uniq > file_unique
```

### Extraire une colonne
```bash
cut -d ',' -f 2 data.csv
```

### Recherche insensible à la casse
```bash
grep -i "error" log.txt
```

### Lignes uniques (apparaissent une seule fois)
```bash
sort file | uniq -u
```

### Filtrer et transformer
```bash
grep "data" file | tr '[:lower:]' '[:upper:]'
```

---

## Exemples Pratiques

### Analyser des logs
```bash
# Trouver les erreurs
grep "ERROR" /var/log/app.log

# Compter les types d'erreurs
grep "ERROR" /var/log/app.log | cut -d ':' -f 2 | sort | uniq -c
```

### Traiter des CSV
```bash
# Extraire la 2ème colonne
cut -d ',' -f 2 data.csv

# Trier par la 3ème colonne
sort -t ',' -k 3 data.csv
```

### Nettoyer du texte
```bash
# Convertir en majuscules
cat file.txt | tr '[:lower:]' '[:upper:]'

# Supprimer les espaces multiples
cat file.txt | tr -s ' '

# Supprimer les lignes vides
grep -v "^$" file.txt
```

### Statistiques sur fichiers
```bash
# Compter les fichiers
find . -type f | wc -l

# Taille totale d'un dossier
du -sh /path/to/dir

# Fichiers les plus volumineux
du -ah /path | sort -hr | head -n 10
```

---

## Ressources

- `man grep` : Manuel de grep
- `man sort` : Manuel de sort
- `man awk` : Outil plus puissant de traitement de texte
- `man sed` : Éditeur de flux (stream editor)
- [Regex101](https://regex101.com/) : Testeur d'expressions régulières
- [ExplainShell](https://explainshell.com/) : Explication des commandes Shell
