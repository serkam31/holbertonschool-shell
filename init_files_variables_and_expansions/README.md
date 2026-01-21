# Shell Init Files, Variables and Expansions

Ce dossier contient 17 scripts qui couvrent les variables d'environnement, les alias, les expansions et les conversions de bases en Shell.

## Objectifs d'apprentissage

- Comprendre les variables locales et globales
- Maîtriser les variables d'environnement
- Utiliser les expansions (arithmétiques, variables, accolades)
- Créer des alias
- Effectuer des conversions de bases numériques
- Manipuler le PATH et les fichiers d'initialisation

---

## Concepts Fondamentaux

### Variables en Shell

Il existe 3 types de variables :

1. **Variables locales** : Visibles uniquement dans le shell courant
   ```bash
   MY_VAR="value"
   ```

2. **Variables d'environnement** : Transmises aux processus enfants
   ```bash
   export MY_VAR="value"
   ```

3. **Variables spéciales** : Définies par le système
   - `$USER` : nom de l'utilisateur
   - `$HOME` : répertoire personnel
   - `$PATH` : chemins de recherche des commandes
   - `$?` : code de retour de la dernière commande
   - `$$` : PID du shell courant

---

### Types d'Expansions

| Type | Syntaxe | Exemple |
|------|---------|---------|
| Variable | `$VAR` ou `${VAR}` | `echo $USER` |
| Commande | `$(cmd)` ou `` `cmd` `` | `echo $(date)` |
| Arithmétique | `$((expression))` | `echo $((2+3))` |
| Accolades | `{a,b,c}` | `echo {1..5}` |
| Tilde | `~` | `cd ~/Documents` |

---

## Liste des Scripts

### 0-alias
**Commande** : `alias ls="rm *"`

**Description** : Crée un alias `ls` qui exécute `rm *` (DANGEREUX - exemple pédagogique).

**Concept** :
- `alias` crée des raccourcis pour des commandes
- Cet exemple montre comment un alias peut masquer une commande existante
- **ATTENTION** : Ne jamais faire cela en pratique !

**Utilisation normale** :
```bash
alias ll="ls -la"
alias gs="git status"
```

---

### 1-hello_you
**Commande** : `echo "hello $USER"`

**Description** : Affiche "hello" suivi du nom de l'utilisateur courant.

**Concept** : Expansion de variable avec `$VARIABLE`.

**Exemple de sortie** :
```
hello john
```

---

### 2-path
**Commande** : `export PATH="$PATH:/action"`

**Description** : Ajoute le répertoire `/action` à la fin de la variable PATH.

**Concept** :
- `PATH` contient les répertoires où le shell cherche les commandes
- On concatène avec `:` comme séparateur
- `export` rend la variable disponible aux processus enfants

---

### 3-paths
**Commande** : `echo $PATH | tr ':' '\n' | wc -l`

**Description** : Compte le nombre de répertoires dans la variable PATH.

**Concept** : Pipeline pour analyser le PATH :
1. `echo $PATH` : affiche le PATH
2. `tr ':' '\n'` : remplace `:` par des retours à la ligne
3. `wc -l` : compte les lignes

---

### 4-global_variables
**Commande** : `printenv`

**Description** : Affiche toutes les variables d'environnement.

**Concept** : `printenv` liste toutes les variables exportées (globales).

**Variables courantes** :
- USER, HOME, PATH, SHELL, PWD, LANG, etc.

---

### 5-local_variables
**Commande** : `set`

**Description** : Affiche toutes les variables (locales et d'environnement) et toutes les fonctions.

**Concept** : `set` affiche TOUT l'environnement du shell (plus complet que `printenv`).

---

### 6-create_local_variable
**Commande** : `BEST="School"`

**Description** : Crée une variable locale nommée `BEST` avec la valeur "School".

**Concept** :
- Variable locale = visible uniquement dans le shell courant
- Pas d'export = pas transmise aux sous-processus

---

### 7-create_global_variable
**Commande** : `export BEST="School"`

**Description** : Crée une variable d'environnement (globale) nommée `BEST`.

**Concept** :
- `export` rend la variable globale
- Elle sera disponible dans tous les processus enfants
- Utilisé pour configurer l'environnement d'exécution

---

### 8-true_knowledge
**Commande** : `echo $((128 + $TRUEKNOWLEDGE))`

**Description** : Additionne 128 à la valeur de la variable TRUEKNOWLEDGE et affiche le résultat.

**Concept** :
- `$(( ))` : expansion arithmétique
- Permet d'effectuer des calculs mathématiques
- Les variables n'ont pas besoin de `$` à l'intérieur

**Exemple** :
```bash
TRUEKNOWLEDGE=10
./8-true_knowledge  # Affiche: 138
```

---

### 9-divide_and_rule
**Commande** : `echo $((POWER / DIVIDE))`

**Description** : Divise POWER par DIVIDE.

**Concept** : Division entière en arithmétique shell.

**Opérateurs disponibles** :
- `+` : addition
- `-` : soustraction
- `*` : multiplication
- `/` : division entière
- `%` : modulo (reste)
- `**` : puissance

---

### 10-love_exponent_breath
**Commande** : `echo $((BREATH ** LOVE))`

**Description** : Calcule BREATH à la puissance LOVE.

**Concept** : `**` est l'opérateur de puissance (exponentiation).

**Exemple** :
```bash
BREATH=2
LOVE=3
./10-love_exponent_breath  # Affiche: 8  (2³ = 8)
```

---

### 11-binary_to_decimal
**Commande** : `echo $((2#$BINARY))`

**Description** : Convertit un nombre binaire (stocké dans BINARY) en décimal.

**Concept** :
- `base#nombre` : spécifie la base d'un nombre
- `2#1010` : 1010 en base 2 (binaire)
- Le shell convertit automatiquement en base 10

**Exemple** :
```bash
BINARY=1010
./11-binary_to_decimal  # Affiche: 10
```

**Bases supportées** :
- `2#` : binaire
- `8#` : octal
- `16#` : hexadécimal

---

### 12-combinations
**Commande** : `echo {a..z}{a..z} | tr ' ' '\n' | grep -v "oo"`

**Description** : Affiche toutes les combinaisons de deux lettres, sauf "oo".

**Concept** :
- `{a..z}{a..z}` : expansion d'accolades (aa ab ac ... zz)
- `tr ' ' '\n'` : met chaque combinaison sur une ligne
- `grep -v "oo"` : exclut "oo"

**Résultat** : aa, ab, ac, ..., om, on, op, ..., zz (sans "oo")

---

### 13-print_float
**Commande** : `printf "%.2f\n" $NUM`

**Description** : Affiche le nombre NUM avec 2 décimales.

**Concept** :
- `printf` : formatage avancé (comme en C)
- `%.2f` : format float avec 2 décimales
- Plus précis que `echo` pour les nombres

**Exemple** :
```bash
NUM=3.14159
./13-print_float  # Affiche: 3.14
```

---

### 14-decimal_to_hexadecimal
**Commande** : `printf "%x\n" $DECIMAL`

**Description** : Convertit un nombre décimal en hexadécimal.

**Concept** :
- `%x` : format hexadécimal minuscule
- `%X` : format hexadécimal majuscule

**Exemple** :
```bash
DECIMAL=255
./14-decimal_to_hexadecimal  # Affiche: ff
```

**Formats printf utiles** :
- `%d` : décimal
- `%x` : hexadécimal
- `%o` : octal
- `%f` : float

---

### 15-rot13
**Commande** : `tr 'A-Za-z' 'N-ZA-Mn-za-m'`

**Description** : Applique le chiffrement ROT13 (rotation de 13 lettres).

**Concept** :
- ROT13 : chiffrement par substitution simple
- A→N, B→O, ..., M→Z, N→A, ..., Z→M
- Chiffrer deux fois = texte original (réversible)

**Exemple** :
```
Entrée : "Hello"
Sortie : "Uryyb"
```

---

### 16-odd
**Commande** : `paste -d, - - | cut -d, -f1`

**Description** : Affiche les lignes impaires (1, 3, 5, 7, ...).

**Concept** :
- `paste -d, - -` : colle 2 lignes consécutives séparées par `,`
- `cut -d, -f1` : garde seulement la première ligne de chaque paire

**Fonctionnement** :
```
Entrée :      Paste :       Cut :
line1         line1,line2   line1
line2         line3,line4   line3
line3         line5,line6   line5
line4
line5
line6
```

---

## Commandes Clés Apprises

| Commande | Description |
|----------|-------------|
| `alias` | Crée un raccourci de commande |
| `export` | Rend une variable globale |
| `printenv` | Affiche les variables d'environnement |
| `set` | Affiche toutes les variables et fonctions |
| `printf` | Formatage avancé de sortie |
| `paste` | Colle des lignes de fichiers |

---

## Variables d'Environnement Importantes

| Variable | Description | Exemple |
|----------|-------------|---------|
| `$USER` | Nom de l'utilisateur | john |
| `$HOME` | Répertoire personnel | /home/john |
| `$PATH` | Chemins de recherche des commandes | /usr/bin:/bin |
| `$PWD` | Répertoire de travail actuel | /home/john/project |
| `$OLDPWD` | Répertoire précédent | /home/john |
| `$SHELL` | Shell par défaut | /bin/bash |
| `$?` | Code retour dernière commande | 0 (succès) |
| `$$` | PID du shell courant | 12345 |
| `$RANDOM` | Nombre aléatoire | 15234 |

---

## Expansions en Détail

### 1. Expansion de Variables

```bash
# Basique
echo $USER

# Avec accolades (recommandé)
echo ${USER}

# Valeur par défaut
echo ${VAR:-default}  # Utilise "default" si VAR est vide

# Sous-chaîne
VAR="Hello World"
echo ${VAR:0:5}  # Affiche: Hello
```

---

### 2. Expansion Arithmétique

```bash
# Addition
echo $((5 + 3))  # 8

# Avec variables
A=10
B=5
echo $((A * B))  # 50

# Incrément
((i++))
((i += 5))

# Comparaison (retourne 0 ou 1)
echo $((10 > 5))  # 1 (vrai)
```

---

### 3. Expansion de Commande

```bash
# Syntaxe moderne (recommandée)
TODAY=$(date +%Y-%m-%d)
FILES=$(ls | wc -l)

# Ancienne syntaxe (backticks)
TODAY=`date +%Y-%m-%d`
```

---

### 4. Expansion d'Accolades

```bash
# Séquences
echo {1..10}        # 1 2 3 4 5 6 7 8 9 10
echo {a..z}         # a b c ... z
echo {01..10}       # 01 02 03 ... 10

# Listes
echo {red,green,blue}  # red green blue

# Combinaisons
echo file{1..3}.{txt,md}
# Résultat: file1.txt file1.md file2.txt file2.md file3.txt file3.md

# Imbrications
echo {A..C}{1..3}  # A1 A2 A3 B1 B2 B3 C1 C2 C3
```

---

### 5. Expansion de Tilde

```bash
~           # /home/user (votre home)
~/Documents # /home/user/Documents
~username   # /home/username (home d'un autre user)
```

---

## Alias Utiles

```bash
# Navigation
alias ..='cd ..'
alias ...='cd ../..'
alias home='cd ~'

# Commandes colorées
alias ls='ls --color=auto'
alias grep='grep --color=auto'

# Raccourcis
alias ll='ls -lah'
alias la='ls -A'
alias l='ls -CF'

# Git
alias gs='git status'
alias ga='git add'
alias gc='git commit'
alias gp='git push'

# Sécurité
alias rm='rm -i'  # Demande confirmation
alias cp='cp -i'
alias mv='mv -i'

# Utilitaires
alias c='clear'
alias h='history'
alias path='echo $PATH | tr ":" "\n"'
```

---

## Fichiers d'Initialisation

### Pour Bash

| Fichier | Type | Quand chargé |
|---------|------|--------------|
| `/etc/profile` | Global | Login shell (tous users) |
| `~/.bash_profile` | User | Login shell |
| `~/.bash_login` | User | Login shell (si pas .bash_profile) |
| `~/.profile` | User | Login shell (si pas les 2 autres) |
| `~/.bashrc` | User | Shell interactif non-login |
| `~/.bash_logout` | User | À la déconnexion |

**Bonne pratique** : Mettre vos configurations dans `~/.bashrc` et sourcer depuis `~/.bash_profile` :

```bash
# Dans ~/.bash_profile
if [ -f ~/.bashrc ]; then
    . ~/.bashrc
fi
```

---

## Conversions de Bases

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

### Conversions en Shell

```bash
# Binaire → Décimal
echo $((2#1010))  # 10

# Octal → Décimal
echo $((8#17))  # 15

# Hexadécimal → Décimal
echo $((16#FF))  # 255

# Décimal → Hexadécimal
printf "%x\n" 255  # ff

# Décimal → Octal
printf "%o\n" 15  # 17

# Décimal → Binaire (avec bc)
echo "obase=2; 10" | bc  # 1010
```

---

## Opérateurs Arithmétiques

| Opérateur | Description | Exemple | Résultat |
|-----------|-------------|---------|----------|
| `+` | Addition | `$((5+3))` | 8 |
| `-` | Soustraction | `$((5-3))` | 2 |
| `*` | Multiplication | `$((5*3))` | 15 |
| `/` | Division entière | `$((10/3))` | 3 |
| `%` | Modulo (reste) | `$((10%3))` | 1 |
| `**` | Puissance | `$((2**3))` | 8 |
| `++` | Incrément | `((i++))` | i = i+1 |
| `--` | Décrément | `((i--))` | i = i-1 |

---

## Exemples Pratiques

### Créer des backups datés
```bash
BACKUP_DIR="backup_$(date +%Y%m%d_%H%M%S)"
mkdir "$BACKUP_DIR"
```

### Boucle avec expansion
```bash
# Créer 10 fichiers
touch file{1..10}.txt

# Renommer en masse
for i in {1..10}; do
    mv "old_$i.txt" "new_$i.txt"
done
```

### Calculs rapides
```bash
# Calculer un pourcentage
TOTAL=1000
PART=250
echo "$(($PART * 100 / $TOTAL))%"  # 25%

# Convertir secondes en minutes
SECONDS=3725
echo "$((SECONDS / 60)) minutes"  # 62 minutes
```

### Configuration PATH personnalisée
```bash
# Ajouter un dossier au PATH
export PATH="$HOME/bin:$PATH"

# Ajouter plusieurs dossiers
export PATH="$HOME/bin:$HOME/.local/bin:$PATH"
```

### Variables temporaires
```bash
# Variable pour une seule commande
DEBUG=1 ./script.sh

# Sauvegarder et restaurer
OLD_PATH=$PATH
export PATH="/tmp/bin:$PATH"
# ... faire quelque chose ...
export PATH=$OLD_PATH
```

---

## Bonnes Pratiques

1. **Toujours utiliser des accolades** : `${VAR}` au lieu de `$VAR`
2. **Quoter les variables** : `"$VAR"` pour éviter les problèmes d'espaces
3. **Exporter uniquement si nécessaire** : Les variables locales sont plus sûres
4. **Noms en MAJUSCULES** : Convention pour les variables d'environnement
5. **Vérifier l'existence** : `${VAR:-default}` pour valeurs par défaut
6. **Éviter les alias dangereux** : Ne jamais masquer des commandes système

---

## Ressources

- `man bash` : Manuel complet de Bash
- `man export` : Variables d'environnement
- `man printf` : Formatage de sortie
- [Bash Hackers Wiki](https://wiki.bash-hackers.org/)
- [Advanced Bash-Scripting Guide](https://tldp.org/LDP/abs/html/)
