# Holberton School - Shell

Ce repository contient tous les projets et exercices liés à l'apprentissage du Shell (Bash) dans le cadre de la formation Holberton School.

## Description

Ce projet couvre les bases essentielles du scripting Shell et de la ligne de commande Unix/Linux. Il est divisé en 4 modules principaux qui permettent d'apprendre progressivement les concepts fondamentaux du Shell.

## Structure du Repository

Le repository est organisé en 4 dossiers principaux :

```
holbertonschool-shell/
├── basics/                                    (18 scripts)
├── permissions/                               (17 scripts)
├── io_redirections_and_filters/              (27 scripts)
└── init_files_variables_and_expansions/      (17 scripts)
```

## Modules

### 1. [Basics](./basics/)
**Objectif** : Apprendre les commandes de base du Shell pour naviguer et manipuler le système de fichiers.

**Concepts couverts** :
- Navigation dans le système de fichiers (`pwd`, `cd`, `ls`)
- Manipulation de fichiers et dossiers (`cp`, `mv`, `rm`, `mkdir`, `rmdir`)
- Liens symboliques
- Détection de types de fichiers
- Copie conditionnelle de fichiers

**Scripts** : 0-17 (18 exercices)

---

### 2. [Permissions](./permissions/)
**Objectif** : Comprendre et maîtriser le système de permissions Unix/Linux.

**Concepts couverts** :
- Gestion des utilisateurs et groupes (`su`, `whoami`, `groups`)
- Modification des permissions (`chmod`)
- Changement de propriétaire (`chown`, `chgrp`)
- Permissions symboliques et octales
- Permissions sur les liens symboliques
- Récursivité et permissions conditionnelles

**Scripts** : 0-16 (17 exercices)

---

### 3. [I/O Redirections and Filters](./io_redirections_and_filters/)
**Objectif** : Maîtriser les redirections d'entrée/sortie et le traitement de texte.

**Concepts couverts** :
- Redirections (`>`, `>>`, `<`, `2>`, `&>`)
- Pipes (`|`) et chaînage de commandes
- Filtres de texte (`cat`, `head`, `tail`, `grep`, `sort`, `uniq`, `cut`, `tr`)
- Recherche de fichiers (`find`)
- Traitement avancé de texte
- Combinaisons complexes de commandes

**Scripts** : 0-26 (27 exercices)

---

### 4. [Init Files, Variables and Expansions](./init_files_variables_and_expansions/)
**Objectif** : Comprendre les variables d'environnement, les alias et les expansions.

**Concepts couverts** :
- Variables locales et globales
- Variables d'environnement (`export`, `printenv`, `set`)
- Alias de commandes
- Expansions arithmétiques (`$(( ))`)
- Expansions de variables (`$VAR`)
- Expansions d'accolades (`{a..z}`)
- Conversions de bases (binaire, décimal, hexadécimal)
- Formatage avec `printf`
- Transformations de texte (ROT13)

**Scripts** : 0-16 (17 exercices)

---

## Compétences Acquises

À la fin de ce projet, vous serez capable de :

- Naviguer efficacement dans un système Unix/Linux
- Gérer les permissions et la sécurité des fichiers
- Automatiser des tâches avec des scripts Bash
- Manipuler et traiter des données textuelles
- Comprendre et utiliser les variables d'environnement
- Créer des pipelines de commandes complexes
- Utiliser les outils standards Unix (coreutils)

## Prérequis

- Système Unix/Linux ou macOS
- Bash (version 4.0 ou supérieure recommandée)
- Accès au terminal

## Utilisation

Chaque script peut être exécuté directement :

```bash
./script_name
```

Ou avec bash :

```bash
bash script_name
```

## Auteur

MARQUES Matéo

## Ressources Utiles

- [Bash Guide for Beginners](https://tldp.org/LDP/Bash-Beginners-Guide/html/)
- [Advanced Bash-Scripting Guide](https://tldp.org/LDP/abs/html/)
- [Explain Shell](https://explainshell.com/) - Pour comprendre les commandes Shell
- [ShellCheck](https://www.shellcheck.net/) - Pour vérifier la syntaxe de vos scripts
