# TP complet — Créer une mini application Python avec OpenClaude gratuit

## Objectif général du TP

Dans ce TP, nous allons créer une mini application graphique en Python avec **Tkinter**.

L’application permettra de gérer une liste de tâches :

```text
1. Ajouter une tâche
2. Afficher les tâches
3. Marquer une tâche comme terminée
4. Supprimer une tâche
5. Effacer toutes les tâches
6. Sauvegarder les tâches dans un fichier JSON
```

Mais l’objectif principal n’est pas seulement de coder l’application.

L’objectif principal est d’apprendre à utiliser un assistant de développement dans le terminal, ici **OpenClaude**, de manière structurée :

```text
1. Créer un projet propre
2. Lancer OpenClaude dans le bon dossier
3. Comprendre les slash commands
4. Comprendre pourquoi /init peut ne pas fonctionner comme dans Claude Code officiel
5. Créer manuellement un bon fichier CLAUDE.md
6. Demander un plan avant de coder
7. Générer une première version du code
8. Tester le programme
9. Corriger les erreurs
10. Ajouter des fonctionnalités progressivement
11. Vérifier les modifications avec git diff
12. Comprendre les différences avec Claude Code officiel
```

---

# 1. Ce que nous allons utiliser

Dans ce TP, nous allons utiliser :

```text
Python
Tkinter
OpenClaude
Ollama
Git
Un fichier CLAUDE.md
Des fichiers Markdown de procédures
```

Nous n’allons pas utiliser :

```text
React
Node.js
npm pour le projet Python
Flask
Django
FastAPI
Docker
Base de données
Framework externe
```

Le but est de rester simple, clair et adapté à des étudiants débutants.

---

# 2. Différence générale entre Claude Code officiel et OpenClaude

Avant de commencer, il faut bien comprendre une chose.

**Claude Code officiel** est l’outil d’Anthropic. Il est conçu pour lire un projet, modifier des fichiers, exécuter des commandes et aider au développement dans un terminal. Sa documentation officielle décrit notamment les slash commands comme des commandes utilisées pour contrôler la session Claude Code. ([Claude][2])

**OpenClaude**, dans ce TP, est une alternative open source qui essaie de reproduire une partie de cette expérience avec différents fournisseurs de modèles, y compris des modèles locaux comme ceux d’Ollama. ([GitHub][1])

Cela veut dire :

```text
Claude Code officiel = plus intégré, plus stable, plus fiable
OpenClaude = plus flexible, gratuit/local possible, mais parfois moins fiable
```

<details>
<summary>Différence avec Claude Code officiel</summary>

Avec Claude Code officiel, certaines commandes comme `/init`, `/help`, `/compact`, `/context`, `/permissions` ou `/diff` sont généralement mieux intégrées à l’outil officiel.

Avec OpenClaude, certaines commandes peuvent exister, mais leur comportement peut varier selon :

```text
- la version installée ;
- le modèle utilisé ;
- le fournisseur configuré ;
- le dossier de travail ;
- les permissions ;
- le système d’exploitation ;
- la qualité du modèle local.
```

Dans votre essai réel, lorsque vous avez tapé `/init`, OpenClaude n’a pas directement créé un bon fichier `CLAUDE.md`. Il a demandé quel codebase il devait analyser, puis il a proposé un contenu générique avec des éléments inutiles pour votre TP, comme des emojis, un placeholder d’image, une section “Contributing” et un style trop proche d’un README général. 

Dans ce TP, nous allons donc faire quelque chose de plus propre et plus pédagogique :

```text
Nous allons créer CLAUDE.md manuellement.
```

</details>

---

# 3. Ce qu’est une slash command

Une **slash command** est une commande qui commence par `/`.

Exemples :

```text
/help
/init
/clear
/provider
/diff
/context
/compact
```

Ces commandes ne sont pas des commandes Python.

Ce sont des commandes données à l’assistant dans le terminal pour contrôler la session.

Par exemple :

```text
/help
```

sert généralement à afficher l’aide.

```text
/init
```

sert généralement, dans Claude Code officiel, à initialiser un projet avec un fichier `CLAUDE.md`. La documentation officielle de Claude Code indique que `/init` initialise le projet avec un guide `CLAUDE.md`. ([Claude][2])

```text
/provider
```

dans OpenClaude peut servir à configurer le fournisseur de modèle, par exemple Ollama ou une API compatible OpenAI. OpenClaude indique que les profils de fournisseurs peuvent être gérés dans l’application avec `/provider`. ([GitHub][1])

---

# 4. Principe pédagogique du TP

Dans ce TP, nous allons suivre une méthode professionnelle :

```text
Contexte clair
        ↓
Plan
        ↓
Code
        ↓
Test
        ↓
Correction
        ↓
Amélioration
        ↓
Vérification
```

Nous ne demandons pas à l’assistant :

```text
Code-moi tout directement.
```

Nous allons plutôt lui donner des instructions progressives.

C’est important, car un assistant de code peut se tromper. Il faut donc garder le contrôle.

---

# 5. Préparer l’environnement

## 5.1 Vérifier Python

Dans le terminal, tapez :

```bash
python --version
```

ou :

```bash
python3 --version
```

Vous devez voir une version de Python, par exemple :

```text
Python 3.11.5
```

Si Python n’est pas installé, il faut l’installer avant de continuer.

---

## 5.2 Vérifier Tkinter

Tkinter est normalement inclus avec Python.

Pour vérifier si Tkinter fonctionne, tapez :

```bash
python -m tkinter
```

ou :

```bash
python3 -m tkinter
```

Si une petite fenêtre s’ouvre, Tkinter fonctionne.

Si vous avez une erreur, cela veut dire que Tkinter n’est pas installé correctement.

Sur Ubuntu/Debian, on peut souvent corriger avec :

```bash
sudo apt install python3-tk
```

Sur Windows et macOS, Tkinter est généralement installé avec Python.

---

## 5.3 Vérifier Git

Nous allons utiliser Git pour vérifier les modifications, surtout parce que `/diff` peut ne pas fonctionner dans OpenClaude comme dans Claude Code officiel.

Tapez :

```bash
git --version
```

Vous devez obtenir quelque chose comme :

```text
git version 2.44.0
```

Si Git n’est pas installé, installez-le avant de continuer.

<details>
<summary>Différence avec Claude Code officiel</summary>

Avec Claude Code officiel, la commande `/diff` peut afficher directement les changements effectués dans le projet.

Avec OpenClaude, `/diff` peut exister ou non selon la version. Pour éviter les surprises, nous allons utiliser aussi Git.

La commande universelle est :

```bash
git diff
```

Elle fonctionne même si l’assistant ne fournit pas de commande `/diff`.

</details>

---

# 6. Installer OpenClaude

Dans le terminal, installez OpenClaude :

```bash
npm install -g @gitlawb/openclaude
```

Même si notre projet est en Python, OpenClaude lui-même s’installe avec npm.

Vérifiez ensuite l’installation :

```bash
openclaude --version
```

Si la commande n’est pas reconnue, fermez et rouvrez le terminal.

<details>
<summary>Différence avec Claude Code officiel</summary>

Avec Claude Code officiel, on lance généralement :

```bash
claude
```

Avec OpenClaude, on lance :

```bash
openclaude
```

Il ne faut pas confondre les deux commandes.

Dans ce TP, nous utilisons :

```bash
openclaude
```

</details>

---

# 7. Installer Ollama pour utiliser un modèle gratuit local

OpenClaude est l’outil de dialogue et de modification de code, mais il lui faut un modèle d’IA.

Pour rester dans une logique gratuite, nous allons utiliser **Ollama**.

Après installation d’Ollama, téléchargez un modèle adapté au code :

```bash
ollama pull qwen2.5-coder:7b
```

Ensuite, testez le modèle :

```bash
ollama run qwen2.5-coder:7b
```

Posez une question simple :

```text
Explique une boucle for en Python.
```

Si le modèle répond, Ollama fonctionne.

Pour quitter :

```text
/bye
```

<details>
<summary>Différence avec Claude Code officiel</summary>

Avec Claude Code officiel, l’outil utilise les modèles Claude d’Anthropic.

Avec OpenClaude, nous pouvons utiliser différents fournisseurs de modèles. OpenClaude mentionne notamment la prise en charge d’Ollama, d’APIs compatibles OpenAI, de Gemini, de GitHub Models et d’autres backends. ([GitHub][1])

Donc :

```text
Claude Code officiel :
- utilise les modèles Claude ;
- généralement plus puissant ;
- plus intégré ;
- souvent lié à un abonnement ou à des limites d’usage.

OpenClaude + Ollama :
- peut tourner localement ;
- peut être gratuit ;
- dépend de la puissance de l’ordinateur ;
- dépend beaucoup du modèle choisi.
```

</details>

---

# 8. Créer le dossier du projet

Nous allons maintenant créer le projet.

Dans le terminal :

```bash
mkdir mini-app-openclaude-python
```

Entrez dans le dossier :

```bash
cd mini-app-openclaude-python
```

Créez le fichier principal :

```bash
touch main.py
```

Sur Windows PowerShell :

```powershell
New-Item main.py
```

La structure actuelle est :

```text
mini-app-openclaude-python/
└── main.py
```

---

# 9. Initialiser Git

Dans le dossier du projet, tapez :

```bash
git init
```

Ensuite :

```bash
git status
```

Vous devriez voir que `main.py` est un fichier non suivi.

Ajoutez-le :

```bash
git add main.py
```

Créez un premier commit :

```bash
git commit -m "Initialisation du projet Python"
```

Si Git demande votre nom ou votre email, configurez-les :

```bash
git config --global user.name "Votre Nom"
git config --global user.email "votre.email@example.com"
```

Puis refaites le commit.

<details>
<summary>Pourquoi utiliser Git dans ce TP ?</summary>

Git permet de voir exactement ce qui change dans les fichiers.

Quand un assistant de code modifie un fichier, il ne faut pas accepter aveuglément.

Nous allons utiliser :

```bash
git diff
```

pour voir les modifications.

C’est une habitude professionnelle très importante.

</details>

---

# 10. Lancer OpenClaude dans le bon dossier

Toujours dans le dossier du projet, lancez :

```bash
openclaude
```

Il est très important de lancer OpenClaude **dans le dossier du projet**.

Le dossier doit contenir :

```text
main.py
```

Plus tard, il contiendra aussi :

```text
CLAUDE.md
tasks.json
procedures/
```

<details>
<summary>Erreur fréquente</summary>

Si vous lancez OpenClaude depuis un mauvais dossier, l’assistant peut ne pas voir vos fichiers.

Par exemple, si vous êtes dans :

```text
C:\Users\VotreNom
```

au lieu de :

```text
C:\Users\VotreNom\mini-app-openclaude-python
```

OpenClaude risque de ne pas comprendre où est votre projet.

Dans le terminal, vérifiez toujours votre emplacement avec :

```bash
pwd
```

Sur Windows PowerShell :

```powershell
Get-Location
```

</details>

---

# 11. Configurer OpenClaude avec Ollama

Selon votre configuration, OpenClaude peut demander un fournisseur de modèle.

Vous pouvez essayer dans OpenClaude :

```text
/provider
```

Choisissez ensuite Ollama si l’option existe.

Si vous préférez configurer par variables d’environnement, utilisez ceci.

Sur macOS/Linux :

```bash
export CLAUDE_CODE_USE_OPENAI=1
export OPENAI_BASE_URL=http://localhost:11434/v1
export OPENAI_MODEL=qwen2.5-coder:7b

openclaude
```

Sur Windows PowerShell :

```powershell
$env:CLAUDE_CODE_USE_OPENAI="1"
$env:OPENAI_BASE_URL="http://localhost:11434/v1"
$env:OPENAI_MODEL="qwen2.5-coder:7b"

openclaude
```

L’idée est de dire à OpenClaude :

```text
Utilise Ollama comme fournisseur local.
Utilise le modèle qwen2.5-coder:7b.
```

<details>
<summary>Différence avec Claude Code officiel</summary>

Avec Claude Code officiel, on n’a généralement pas besoin de configurer `OPENAI_BASE_URL` ou `OPENAI_MODEL`.

Avec OpenClaude + Ollama, il faut parfois indiquer :

```text
1. Le fournisseur
2. L’URL locale
3. Le modèle
```

Ici, l’URL locale d’Ollama est généralement :

```text
http://localhost:11434
```

Et l’API compatible OpenAI est souvent exposée sur :

```text
http://localhost:11434/v1
```

</details>

---

# 12. Découvrir les commandes disponibles

Dans OpenClaude, tapez :

```text
/help
```

Observez la réponse.

Ensuite, tapez simplement :

```text
/
```

L’objectif est de voir si OpenClaude affiche une liste de slash commands.

Il faut retenir ceci :

```text
La liste exacte des commandes peut changer selon l’outil et la version.
```

Donc la méthode correcte est :

```text
Je tape / pour voir les commandes disponibles dans ma session.
```

<details>
<summary>Différence avec Claude Code officiel</summary>

Dans Claude Code officiel, la documentation indique que les slash commands sont des commandes pour contrôler la session, et que certaines commandes, comme `/init`, sont intégrées. ([Claude][2])

Avec OpenClaude, le principe existe, mais toutes les commandes ne sont pas forcément identiques.

Donc, dans ce TP, nous utilisons deux méthodes :

```text
1. Slash commands quand elles fonctionnent.
2. Prompts explicites quand elles ne fonctionnent pas.
```

</details>

---

# 13. Pourquoi nous n’allons pas utiliser `/init` directement

Dans Claude Code officiel, `/init` est censé initialiser le projet avec un fichier `CLAUDE.md`. ([Claude][2])

Mais dans notre essai OpenClaude, `/init` a donné un résultat qui n’est pas adapté à notre TP.

Il a répondu qu’il devait savoir quel codebase analyser. Ensuite, quand le contexte a été donné, il a produit un contenu trop général, avec une présentation marketing et des éléments qui ne correspondent pas à une mini application Python débutante. 

Donc, pour ce TP, nous allons faire plus fiable :

```text
Nous allons créer CLAUDE.md nous-mêmes.
```

---

# 14. Créer manuellement CLAUDE.md

Dans un autre terminal, toujours dans le dossier du projet :

```bash
touch CLAUDE.md
```

Sur Windows PowerShell :

```powershell
New-Item CLAUDE.md
```

La structure devient :

```text
mini-app-openclaude-python/
├── CLAUDE.md
└── main.py
```

Ouvrez le dossier dans VS Code :

```bash
code .
```

Puis ouvrez `CLAUDE.md`.

Collez ce contenu :

````markdown
# CLAUDE.md — Instructions du projet

## 1. Contexte du projet

Ce projet est une mini application Python destinée à des étudiants débutants.

L’application utilise Tkinter, la bibliothèque graphique standard de Python.

Le fichier principal du projet est :

```text
main.py
````

L’objectif est de créer progressivement une petite application graphique de gestion de tâches.

## 2. Objectifs pédagogiques

Ce projet doit permettre d’apprendre :

* la structure d’un programme Python simple ;
* l’utilisation de Tkinter ;
* la création d’une fenêtre graphique ;
* l’utilisation des widgets Entry, Button, Label et Listbox ;
* la gestion d’événements avec des fonctions ;
* la lecture progressive du code ;
* l’amélioration d’un programme étape par étape ;
* l’utilisation d’un assistant de code de façon contrôlée ;
* la vérification des modifications avec Git.

## 3. Contraintes importantes

Respecter obligatoirement les règles suivantes :

* utiliser uniquement Python ;
* utiliser uniquement Tkinter pour l’interface graphique ;
* ne pas utiliser React ;
* ne pas utiliser Flask ;
* ne pas utiliser Django ;
* ne pas utiliser FastAPI ;
* ne pas ajouter de dépendances externes ;
* ne pas créer une architecture complexe ;
* garder le projet simple pour des débutants ;
* écrire du code lisible ;
* ajouter des commentaires pédagogiques ;
* expliquer chaque modification ;
* demander un plan avant les modifications importantes.

## 4. Structure du projet

Structure attendue au départ :

```text
mini-app-openclaude-python/
├── CLAUDE.md
└── main.py
```

Si une sauvegarde est ajoutée plus tard, le fichier suivant peut être créé :

```text
tasks.json
```

Si des procédures sont ajoutées plus tard, le dossier suivant peut être créé :

```text
procedures/
```

## 5. Commande pour lancer l’application

Pour exécuter l’application :

```bash
python main.py
```

Sur certains systèmes :

```bash
python3 main.py
```

## 6. Style de code attendu

Le code doit être :

* simple ;
* clair ;
* commenté ;
* adapté à un public débutant ;
* écrit dans un seul fichier au départ ;
* organisé avec des fonctions simples.

Éviter les classes au début, sauf si elles sont demandées explicitement.

## 7. Fonctionnalités attendues pour la version 1

La première version de l’application doit contenir :

* une fenêtre principale Tkinter ;
* un titre ;
* un champ de saisie pour écrire une tâche ;
* un bouton Ajouter ;
* une Listbox pour afficher les tâches ;
* un bouton Marquer comme terminée ;
* un bouton Supprimer.

## 8. Règles pour les réponses de l’assistant

Quand une modification est demandée :

1. Lire le fichier concerné.
2. Proposer un mini-plan.
3. Modifier le code simplement.
4. Expliquer les changements.
5. Donner la commande pour tester.
6. Mentionner les erreurs possibles.
7. Garder un langage pédagogique.
8. Ne pas ajouter de complexité inutile.

## 9. Ce qu’il ne faut pas faire

Ne pas transformer ce projet en application professionnelle complexe.

Ne pas ajouter :

* base de données ;
* serveur web ;
* API ;
* framework externe ;
* architecture multi-dossiers ;
* authentification ;
* Docker ;
* React ;
* npm.

Le but est d’apprendre progressivement Python et Tkinter.

````

---

# 15. Ajouter CLAUDE.md à Git

Dans le terminal :

```bash
git status
````

Vous devriez voir :

```text
Untracked files:
  CLAUDE.md
```

Ajoutez le fichier :

```bash
git add CLAUDE.md
```

Créez un commit :

```bash
git commit -m "Ajout des instructions projet dans CLAUDE.md"
```

---

# 16. Demander à OpenClaude de lire CLAUDE.md

Retournez dans OpenClaude.

Tapez :

```text
Lis le fichier CLAUDE.md et résume les règles principales du projet en 5 points.
Ensuite, attends ma prochaine instruction.
```

Réponse attendue :

```text
1. Le projet est une mini application Python Tkinter.
2. Le fichier principal est main.py.
3. Le code doit rester simple et adapté à des débutants.
4. Aucune dépendance externe ne doit être ajoutée.
5. Chaque modification doit être expliquée.
```

Si OpenClaude donne une réponse trop longue, ce n’est pas grave.

L’important est qu’il ait lu les consignes.

<details>
<summary>Différence avec Claude Code officiel</summary>

Dans Claude Code officiel, `CLAUDE.md` est utilisé comme mémoire de projet. La documentation officielle explique que les fichiers mémoire comme `CLAUDE.md` permettent à Claude de comprendre les conventions, commandes et règles du projet. ([Claude][3])

Avec OpenClaude, selon la version, le fichier peut ne pas être chargé automatiquement de façon aussi fiable.

Donc, dans ce TP, nous demandons explicitement :

```text
Lis CLAUDE.md.
```

Cela évite toute ambiguïté.

</details>

---

# 17. Demander un plan avant de coder

Dans OpenClaude, tapez :

```text
Avant de coder, propose un plan simple pour créer la version 1 de l’application.

Objectif :
Créer une mini application Python Tkinter de gestion de tâches.

Contraintes :
- utiliser main.py ;
- utiliser Tkinter ;
- ne pas créer d’autres fichiers ;
- garder le code simple ;
- ajouter des commentaires pédagogiques ;
- respecter CLAUDE.md ;
- ne pas utiliser de classes pour l’instant.
```

Réponse attendue :

```text
1. Importer tkinter et messagebox.
2. Créer une fenêtre principale.
3. Ajouter un titre.
4. Ajouter un champ de saisie Entry.
5. Ajouter une Listbox pour afficher les tâches.
6. Créer une fonction ajouter_tache().
7. Créer une fonction terminer_tache().
8. Créer une fonction supprimer_tache().
9. Ajouter les boutons.
10. Lancer fenetre.mainloop().
```

---

# 18. Pourquoi demander un plan ?

Demander un plan avant de coder permet de vérifier si l’assistant a compris la tâche.

Si le plan contient :

```text
React
Flask
Django
FastAPI
base de données
serveur web
```

alors il faut l’arrêter immédiatement.

Il faut lui répondre :

```text
Non. Respecte CLAUDE.md. Le projet doit rester en Python Tkinter uniquement.
```

<details>
<summary>Différence avec Claude Code officiel</summary>

Avec Claude Code officiel, on pourrait utiliser une commande comme :

```text
/plan créer une mini application Python Tkinter de gestion de tâches
```

si cette commande est disponible dans la session.

Avec OpenClaude, `/plan` peut ne pas être disponible ou peut ne pas fonctionner pareil.

Donc, la méthode robuste est d’écrire simplement :

```text
Avant de coder, propose un plan simple...
```

Le résultat pédagogique est le même.

</details>

---

# 19. Demander la création de la version 1

Dans OpenClaude, tapez :

```text
Crée maintenant la version 1 de l’application dans main.py.

Contraintes :
- utilise Python avec Tkinter ;
- crée une seule fenêtre principale ;
- ajoute un titre ;
- ajoute un champ Entry pour écrire une tâche ;
- ajoute un bouton Ajouter ;
- ajoute une Listbox pour afficher les tâches ;
- ajoute un bouton Marquer comme terminée ;
- ajoute un bouton Supprimer ;
- garde le code très simple ;
- ajoute des commentaires pédagogiques ;
- ne crée pas d’autre fichier pour l’instant ;
- respecte CLAUDE.md.
```

OpenClaude doit modifier `main.py`.

---

# 20. Vérifier le contenu de main.py

Ouvrez `main.py`.

Le code attendu doit ressembler à ceci :

```python
import tkinter as tk
from tkinter import messagebox


# Fonction appelée quand l'utilisateur clique sur le bouton "Ajouter"
def ajouter_tache():
    # On récupère le texte écrit dans le champ de saisie
    texte = entree_tache.get()

    # On vérifie que le texte n'est pas vide
    if texte.strip() == "":
        messagebox.showwarning("Attention", "Veuillez écrire une tâche.")
        return

    # On ajoute la tâche dans la liste
    liste_taches.insert(tk.END, texte)

    # On vide le champ de saisie après l'ajout
    entree_tache.delete(0, tk.END)


# Fonction appelée pour marquer une tâche comme terminée
def terminer_tache():
    # On récupère la tâche sélectionnée
    selection = liste_taches.curselection()

    # Si aucune tâche n'est sélectionnée, on affiche un message
    if not selection:
        messagebox.showwarning("Attention", "Veuillez sélectionner une tâche.")
        return

    # On récupère l'index de la tâche sélectionnée
    index = selection[0]

    # On récupère le texte de la tâche
    tache = liste_taches.get(index)

    # On évite d'ajouter deux fois le texte [Terminée]
    if not tache.startswith("[Terminée] "):
        liste_taches.delete(index)
        liste_taches.insert(index, "[Terminée] " + tache)


# Fonction appelée pour supprimer une tâche
def supprimer_tache():
    # On récupère la tâche sélectionnée
    selection = liste_taches.curselection()

    # Si aucune tâche n'est sélectionnée, on affiche un message
    if not selection:
        messagebox.showwarning("Attention", "Veuillez sélectionner une tâche.")
        return

    # On supprime la tâche sélectionnée
    index = selection[0]
    liste_taches.delete(index)


# Création de la fenêtre principale
fenetre = tk.Tk()
fenetre.title("Mini Gestionnaire de Tâches")
fenetre.geometry("500x400")

# Titre de l'application
titre = tk.Label(
    fenetre,
    text="Gestionnaire de tâches",
    font=("Arial", 18, "bold")
)
titre.pack(pady=10)

# Champ de saisie pour écrire une tâche
entree_tache = tk.Entry(fenetre, width=40, font=("Arial", 12))
entree_tache.pack(pady=10)

# Bouton pour ajouter une tâche
bouton_ajouter = tk.Button(
    fenetre,
    text="Ajouter",
    width=20,
    command=ajouter_tache
)
bouton_ajouter.pack(pady=5)

# Liste qui affiche les tâches
liste_taches = tk.Listbox(fenetre, width=50, height=10, font=("Arial", 12))
liste_taches.pack(pady=10)

# Bouton pour marquer une tâche comme terminée
bouton_terminer = tk.Button(
    fenetre,
    text="Marquer comme terminée",
    width=25,
    command=terminer_tache
)
bouton_terminer.pack(pady=5)

# Bouton pour supprimer une tâche
bouton_supprimer = tk.Button(
    fenetre,
    text="Supprimer",
    width=25,
    command=supprimer_tache
)
bouton_supprimer.pack(pady=5)

# Lancement de la boucle principale de l'application
fenetre.mainloop()
```

---

# 21. Comprendre le code généré

## 21.1 Les imports

```python
import tkinter as tk
from tkinter import messagebox
```

La ligne :

```python
import tkinter as tk
```

importe la bibliothèque Tkinter et lui donne le nom court `tk`.

Cela permet d’écrire :

```python
tk.Tk()
tk.Label()
tk.Button()
tk.Entry()
tk.Listbox()
```

La ligne :

```python
from tkinter import messagebox
```

permet d’utiliser des boîtes de dialogue comme :

```python
messagebox.showwarning()
messagebox.askyesno()
```

---

## 21.2 La fonction ajouter_tache()

```python
def ajouter_tache():
    texte = entree_tache.get()
```

Cette fonction récupère ce que l’utilisateur a écrit dans le champ de saisie.

```python
if texte.strip() == "":
```

Cette condition vérifie si le texte est vide.

La méthode `.strip()` enlève les espaces au début et à la fin.

Donc si l’utilisateur écrit seulement des espaces, c’est considéré comme vide.

```python
liste_taches.insert(tk.END, texte)
```

Cette ligne ajoute la tâche à la fin de la liste.

```python
entree_tache.delete(0, tk.END)
```

Cette ligne vide le champ après l’ajout.

---

## 21.3 La fonction terminer_tache()

```python
selection = liste_taches.curselection()
```

Cette ligne récupère la tâche sélectionnée.

Si aucune tâche n’est sélectionnée :

```python
if not selection:
```

on affiche un message d’avertissement.

Ensuite :

```python
index = selection[0]
tache = liste_taches.get(index)
```

On récupère l’indice de la tâche et son texte.

Puis :

```python
if not tache.startswith("[Terminée] "):
```

On vérifie si la tâche n’est pas déjà terminée.

Si elle n’est pas terminée, on remplace :

```text
Acheter du lait
```

par :

```text
[Terminée] Acheter du lait
```

---

## 21.4 La fonction supprimer_tache()

Cette fonction supprime la tâche sélectionnée.

```python
liste_taches.delete(index)
```

supprime l’élément à l’indice choisi.

---

## 21.5 La fenêtre principale

```python
fenetre = tk.Tk()
```

Cette ligne crée la fenêtre principale.

```python
fenetre.title("Mini Gestionnaire de Tâches")
```

définit le titre de la fenêtre.

```python
fenetre.geometry("500x400")
```

définit la taille de la fenêtre.

---

## 21.6 Les widgets

Un widget est un élément graphique.

Dans ce programme, nous utilisons :

```text
Label   → afficher du texte
Entry   → saisir du texte
Button  → cliquer sur une action
Listbox → afficher une liste
```

---

## 21.7 La boucle principale

```python
fenetre.mainloop()
```

Cette ligne garde la fenêtre ouverte.

Sans cette ligne, la fenêtre s’ouvrirait puis se fermerait immédiatement.

---

# 22. Vérifier les modifications avec Git

Dans le terminal :

```bash
git status
```

Vous devriez voir que `main.py` a été modifié.

Pour voir les modifications :

```bash
git diff
```

Git affiche ce qui a été ajouté ou modifié.

Si le code est correct, ajoutez-le :

```bash
git add main.py
```

Puis créez un commit :

```bash
git commit -m "Création de la version 1 de l'application Tkinter"
```

<details>
<summary>Différence avec Claude Code officiel</summary>

Avec Claude Code officiel, vous pourriez utiliser :

```text
/diff
```

pour voir les modifications directement dans l’outil.

Avec OpenClaude, la commande `/diff` peut ne pas fonctionner ou ne pas être disponible.

Donc, dans ce TP, nous utilisons :

```bash
git diff
```

C’est plus universel et plus professionnel.

</details>

---

# 23. Tester l’application

Dans le terminal :

```bash
python main.py
```

ou :

```bash
python3 main.py
```

Une fenêtre doit s’ouvrir.

Testez :

```text
1. Écrivez : Acheter du lait
2. Cliquez sur Ajouter
3. Sélectionnez la tâche
4. Cliquez sur Marquer comme terminée
5. Sélectionnez la tâche
6. Cliquez sur Supprimer
```

---

# 24. Erreurs fréquentes

## Erreur 1 — Tkinter n’est pas installé

Message possible :

```text
ModuleNotFoundError: No module named 'tkinter'
```

Solution Ubuntu/Debian :

```bash
sudo apt install python3-tk
```

---

## Erreur 2 — Mauvais nom de variable

Message possible :

```text
NameError: name 'entree_tache' is not defined
```

Cause probable :

```text
La fonction utilise entree_tache avant que la variable existe,
ou le nom a été écrit différemment.
```

Correction :

```text
Vérifier que le champ s’appelle toujours entree_tache partout.
```

---

## Erreur 3 — Le fichier main.py est vide

Cause possible :

```text
OpenClaude n’a pas modifié le bon fichier.
```

Correction :

```text
Vérifier que OpenClaude a été lancé dans le bon dossier.
```

---

# 25. Corriger une erreur avec OpenClaude

Si une erreur apparaît, copiez-la entièrement.

Dans OpenClaude, écrivez :

```text
Voici l’erreur obtenue quand je lance python main.py :

COLLER L’ERREUR ICI

Corrige le fichier main.py.
Explique simplement la cause de l’erreur.
Respecte CLAUDE.md.
Garde le code adapté à des débutants.
```

Exemple :

```text
Voici l’erreur obtenue quand je lance python main.py :

NameError: name 'liste_taches' is not defined

Corrige le fichier main.py.
Explique simplement la cause de l’erreur.
Respecte CLAUDE.md.
Garde le code adapté à des débutants.
```

---

# 26. Ajouter une fonctionnalité : effacer toutes les tâches

Nous allons maintenant améliorer l’application.

Objectif :

```text
Ajouter un bouton "Effacer toutes les tâches".
```

Dans OpenClaude, tapez :

```text
Avant de modifier le code, propose un mini-plan pour ajouter un bouton "Effacer toutes les tâches".

Contraintes :
- utiliser messagebox.askyesno pour demander confirmation ;
- supprimer toutes les tâches seulement si l’utilisateur confirme ;
- garder le code simple ;
- respecter CLAUDE.md.
```

Attendez le plan.

Ensuite, tapez :

```text
Applique ce plan dans main.py.

Fonctionnalité :
- Ajouter un bouton "Effacer toutes les tâches".
- Quand on clique dessus, afficher une confirmation.
- Si l’utilisateur confirme, supprimer toutes les tâches de la Listbox.
- Ajouter des commentaires pédagogiques.
- Respecter CLAUDE.md.
```

---

# 27. Code attendu pour effacer toutes les tâches

OpenClaude devrait ajouter une fonction comme :

```python
def effacer_toutes_les_taches():
    # On demande confirmation avant d'effacer toutes les tâches
    confirmation = messagebox.askyesno(
        "Confirmation",
        "Voulez-vous vraiment effacer toutes les tâches ?"
    )

    # Si l'utilisateur confirme, on supprime toutes les tâches
    if confirmation:
        liste_taches.delete(0, tk.END)
```

Et un bouton :

```python
bouton_effacer = tk.Button(
    fenetre,
    text="Effacer toutes les tâches",
    width=25,
    command=effacer_toutes_les_taches
)
bouton_effacer.pack(pady=5)
```

---

# 28. Tester la nouvelle fonctionnalité

Lancez :

```bash
python main.py
```

Testez :

```text
1. Ajoutez trois tâches.
2. Cliquez sur Effacer toutes les tâches.
3. Une confirmation doit apparaître.
4. Cliquez sur Non.
5. Les tâches doivent rester.
6. Cliquez encore sur Effacer toutes les tâches.
7. Cliquez sur Oui.
8. Les tâches doivent disparaître.
```

Ensuite :

```bash
git diff
```

Si tout est correct :

```bash
git add main.py
git commit -m "Ajout du bouton pour effacer toutes les tâches"
```

---

# 29. Ajouter une sauvegarde JSON

Maintenant, nous allons sauvegarder les tâches.

Objectif :

```text
Quand on ferme l’application et qu’on la relance,
les tâches doivent encore être là.
```

Nous allons utiliser un fichier :

```text
tasks.json
```

Dans OpenClaude, tapez :

```text
Avant de modifier le code, propose un mini-plan pour ajouter une sauvegarde JSON.

Contraintes :
- utiliser le module standard json ;
- créer un fichier tasks.json ;
- sauvegarder après ajout ;
- sauvegarder après suppression ;
- sauvegarder après marquage terminé ;
- sauvegarder après effacement total ;
- charger les tâches au démarrage ;
- garder le code simple ;
- respecter CLAUDE.md.
```

Après le plan, tapez :

```text
Applique ce plan dans main.py.

Ajoute une sauvegarde des tâches dans tasks.json.

Contraintes :
- Quand on ajoute une tâche, elle est sauvegardée.
- Quand on supprime une tâche, le fichier est mis à jour.
- Quand on marque une tâche comme terminée, le fichier est mis à jour.
- Quand on efface toutes les tâches, le fichier est mis à jour.
- Quand on ouvre l’application, les tâches existantes sont chargées.
- Utilise uniquement les modules standards de Python.
- Garde le code simple pour débutants.
- Respecte CLAUDE.md.
```

---

# 30. Code attendu pour la sauvegarde JSON

Le code devrait ajouter :

```python
import json
```

Puis :

```python
FICHIER_TACHES = "tasks.json"
```

Puis une fonction de sauvegarde :

```python
def sauvegarder_taches():
    """
    Sauvegarde toutes les tâches affichées dans la Listbox
    dans un fichier JSON.
    """
    taches = liste_taches.get(0, tk.END)

    with open(FICHIER_TACHES, "w", encoding="utf-8") as fichier:
        json.dump(list(taches), fichier, ensure_ascii=False, indent=4)
```

Puis une fonction de chargement :

```python
def charger_taches():
    """
    Charge les tâches depuis le fichier JSON si ce fichier existe.
    """
    try:
        with open(FICHIER_TACHES, "r", encoding="utf-8") as fichier:
            taches = json.load(fichier)

            for tache in taches:
                liste_taches.insert(tk.END, tache)

    except FileNotFoundError:
        pass
```

Attention : `charger_taches()` doit être appelé après la création de `liste_taches`.

Donc l’ordre doit être :

```text
1. Créer la fenêtre
2. Créer la Listbox
3. Appeler charger_taches()
4. Lancer fenetre.mainloop()
```

---

# 31. Code complet final possible

Voici une version complète possible de `main.py` après toutes les améliorations :

```python
import json
import tkinter as tk
from tkinter import messagebox


# Nom du fichier utilisé pour sauvegarder les tâches
FICHIER_TACHES = "tasks.json"


def sauvegarder_taches():
    """
    Sauvegarde toutes les tâches affichées dans la Listbox
    dans un fichier JSON.
    """
    taches = liste_taches.get(0, tk.END)

    with open(FICHIER_TACHES, "w", encoding="utf-8") as fichier:
        json.dump(list(taches), fichier, ensure_ascii=False, indent=4)


def charger_taches():
    """
    Charge les tâches depuis le fichier JSON si ce fichier existe.
    """
    try:
        with open(FICHIER_TACHES, "r", encoding="utf-8") as fichier:
            taches = json.load(fichier)

            for tache in taches:
                liste_taches.insert(tk.END, tache)

    except FileNotFoundError:
        # Si le fichier n'existe pas encore, ce n'est pas une erreur.
        # Cela arrive simplement au premier lancement de l'application.
        pass


def ajouter_tache():
    """
    Ajoute une nouvelle tâche dans la liste.
    """
    texte = entree_tache.get()

    if texte.strip() == "":
        messagebox.showwarning("Attention", "Veuillez écrire une tâche.")
        return

    liste_taches.insert(tk.END, texte)
    entree_tache.delete(0, tk.END)

    sauvegarder_taches()


def terminer_tache():
    """
    Marque la tâche sélectionnée comme terminée.
    """
    selection = liste_taches.curselection()

    if not selection:
        messagebox.showwarning("Attention", "Veuillez sélectionner une tâche.")
        return

    index = selection[0]
    tache = liste_taches.get(index)

    if not tache.startswith("[Terminée] "):
        liste_taches.delete(index)
        liste_taches.insert(index, "[Terminée] " + tache)

    sauvegarder_taches()


def supprimer_tache():
    """
    Supprime la tâche sélectionnée.
    """
    selection = liste_taches.curselection()

    if not selection:
        messagebox.showwarning("Attention", "Veuillez sélectionner une tâche.")
        return

    index = selection[0]
    liste_taches.delete(index)

    sauvegarder_taches()


def effacer_toutes_les_taches():
    """
    Efface toutes les tâches après confirmation.
    """
    confirmation = messagebox.askyesno(
        "Confirmation",
        "Voulez-vous vraiment effacer toutes les tâches ?"
    )

    if confirmation:
        liste_taches.delete(0, tk.END)
        sauvegarder_taches()


# Création de la fenêtre principale
fenetre = tk.Tk()
fenetre.title("Mini Gestionnaire de Tâches")
fenetre.geometry("500x450")

# Titre de l'application
titre = tk.Label(
    fenetre,
    text="Gestionnaire de tâches",
    font=("Arial", 18, "bold")
)
titre.pack(pady=10)

# Champ de saisie
entree_tache = tk.Entry(fenetre, width=40, font=("Arial", 12))
entree_tache.pack(pady=10)

# Bouton Ajouter
bouton_ajouter = tk.Button(
    fenetre,
    text="Ajouter",
    width=25,
    command=ajouter_tache
)
bouton_ajouter.pack(pady=5)

# Liste des tâches
liste_taches = tk.Listbox(fenetre, width=50, height=10, font=("Arial", 12))
liste_taches.pack(pady=10)

# Bouton Terminer
bouton_terminer = tk.Button(
    fenetre,
    text="Marquer comme terminée",
    width=25,
    command=terminer_tache
)
bouton_terminer.pack(pady=5)

# Bouton Supprimer
bouton_supprimer = tk.Button(
    fenetre,
    text="Supprimer",
    width=25,
    command=supprimer_tache
)
bouton_supprimer.pack(pady=5)

# Bouton Effacer tout
bouton_effacer = tk.Button(
    fenetre,
    text="Effacer toutes les tâches",
    width=25,
    command=effacer_toutes_les_taches
)
bouton_effacer.pack(pady=5)

# Chargement des tâches sauvegardées
charger_taches()

# Lancement de l'application
fenetre.mainloop()
```

---

# 32. Tester la sauvegarde

Lancez :

```bash
python main.py
```

Ajoutez :

```text
Réviser Python
Préparer le TP
Lire CLAUDE.md
```

Fermez la fenêtre.

Relancez :

```bash
python main.py
```

Les tâches doivent réapparaître.

Un fichier doit être créé :

```text
tasks.json
```

Son contenu peut ressembler à ceci :

```json
[
    "Réviser Python",
    "[Terminée] Préparer le TP",
    "Lire CLAUDE.md"
]
```

---

# 33. Vérifier les modifications après sauvegarde

Dans le terminal :

```bash
git status
```

Vous devriez voir :

```text
modified: main.py
untracked: tasks.json
```

Pour voir le code modifié :

```bash
git diff main.py
```

Pour ajouter le code :

```bash
git add main.py
```

Il est possible de ne pas ajouter `tasks.json`, car c’est un fichier de données généré.

Pour l’ignorer, créez un fichier `.gitignore` :

```bash
touch .gitignore
```

Sur Windows :

```powershell
New-Item .gitignore
```

Ajoutez dedans :

```text
tasks.json
__pycache__/
*.pyc
```

Puis :

```bash
git add .gitignore
git commit -m "Ajout de la sauvegarde JSON des tâches"
```

---

# 34. Créer des procédures réutilisables

Dans Claude Code officiel, on peut créer des skills ou commandes personnalisées. La documentation officielle indique que les skills peuvent être créées avec un fichier `SKILL.md` et invoquées directement avec `/skill-name`. Elle indique aussi que les anciennes commandes personnalisées dans `.claude/commands/` continuent de fonctionner, mais que les commandes personnalisées ont été fusionnées avec le système de skills. ([Claude][3])

Avec OpenClaude, pour un TP fiable, nous allons utiliser des fichiers Markdown de procédure.

Créez un dossier :

```bash
mkdir procedures
```

Créez un fichier :

```bash
touch procedures/python-feature.md
```

Sur Windows :

```powershell
New-Item -ItemType Directory procedures
New-Item procedures/python-feature.md
```

Ajoutez :

```markdown
# Procédure — Ajouter une fonctionnalité Python Tkinter

Tu dois ajouter une fonctionnalité dans une application Python Tkinter.

## Règles obligatoires

1. Lire CLAUDE.md.
2. Lire main.py.
3. Comprendre la structure existante.
4. Proposer un mini-plan.
5. Modifier le code simplement.
6. Ne pas ajouter de dépendance externe.
7. Ajouter des commentaires pédagogiques.
8. Expliquer les changements.
9. Donner la commande pour tester.

## Style attendu

Le code doit rester adapté à des étudiants débutants.

Il faut éviter :

- les classes complexes ;
- les architectures avancées ;
- les dépendances externes ;
- les frameworks web ;
- les modifications inutiles.
```

Utilisation dans OpenClaude :

```text
Lis procedures/python-feature.md et applique cette procédure.

Fonctionnalité à ajouter :
Ajouter un bouton qui affiche le nombre total de tâches dans une messagebox.
```

<details>
<summary>Différence avec Claude Code officiel</summary>

Avec Claude Code officiel, on pourrait créer une vraie skill :

```text
.claude/skills/python-feature/SKILL.md
```

Puis l’appeler ainsi :

```text
/python-feature ajouter un bouton qui affiche le nombre total de tâches
```

Avec OpenClaude, pour éviter les problèmes de compatibilité, nous utilisons :

```text
procedures/python-feature.md
```

et nous demandons explicitement :

```text
Lis ce fichier et applique cette procédure.
```

C’est moins automatique, mais plus robuste pour un cours.

</details>

---

# 35. Créer une procédure pour expliquer le code

Créez :

```bash
touch procedures/explain-python.md
```

Sur Windows :

```powershell
New-Item procedures/explain-python.md
```

Ajoutez :

```markdown
# Procédure — Expliquer du code Python

Tu dois expliquer du code Python à des étudiants débutants.

## Structure obligatoire

1. Rôle général du programme.
2. Explication des imports.
3. Explication des constantes.
4. Explication des variables importantes.
5. Explication de chaque fonction.
6. Explication des widgets Tkinter.
7. Explication des événements.
8. Explication du fichier JSON.
9. Erreurs fréquentes.
10. Résumé final simple.

## Style

- utiliser un langage simple ;
- éviter le jargon inutile ;
- expliquer ligne par ligne si nécessaire ;
- donner des exemples concrets ;
- rester pédagogique ;
- ne pas supposer que les étudiants connaissent déjà Tkinter.
```

Utilisation dans OpenClaude :

```text
Lis procedures/explain-python.md et explique main.py selon cette procédure.
```

---

# 36. Créer une procédure pour corriger les erreurs

Créez :

```bash
touch procedures/debug-python.md
```

Sur Windows :

```powershell
New-Item procedures/debug-python.md
```

Ajoutez :

```markdown
# Procédure — Corriger une erreur Python

Tu dois aider à corriger une erreur dans une application Python Tkinter.

## Étapes obligatoires

1. Lire CLAUDE.md.
2. Lire main.py.
3. Lire le message d’erreur fourni.
4. Identifier la ligne ou la cause probable.
5. Expliquer l’erreur en langage simple.
6. Proposer une correction minimale.
7. Modifier seulement ce qui est nécessaire.
8. Donner la commande pour tester.
9. Mentionner comment éviter cette erreur à l’avenir.

## Contraintes

- garder le code simple ;
- ne pas réécrire toute l’application sans raison ;
- ne pas ajouter de dépendance externe ;
- respecter le niveau débutant.
```

Utilisation :

```text
Lis procedures/debug-python.md et applique cette procédure.

Erreur obtenue :

COLLER L’ERREUR ICI
```

---

# 37. Ajouter les procédures à Git

Dans le terminal :

```bash
git status
```

Ajoutez :

```bash
git add procedures/
```

Puis :

```bash
git commit -m "Ajout des procédures pédagogiques pour OpenClaude"
```

---

# 38. Structure finale du projet

À la fin, le projet peut ressembler à ceci :

```text
mini-app-openclaude-python/
├── .git/
├── .gitignore
├── CLAUDE.md
├── main.py
└── procedures/
    ├── python-feature.md
    ├── explain-python.md
    └── debug-python.md
```

Le fichier `tasks.json` peut exister localement, mais il est ignoré par Git :

```text
tasks.json
```

---

# 39. Résumé des commandes utilisées

## Commandes système

```bash
mkdir mini-app-openclaude-python
cd mini-app-openclaude-python
touch main.py
touch CLAUDE.md
python main.py
git init
git status
git diff
git add .
git commit -m "message"
```

## Commandes OpenClaude possibles

```text
/help
/
 /provider
/clear
```

Selon la version, d’autres commandes peuvent être disponibles.

## Prompts importants

```text
Lis CLAUDE.md et respecte ses consignes.
```

```text
Avant de coder, propose un mini-plan.
```

```text
Corrige cette erreur en gardant le code simple.
```

```text
Lis procedures/python-feature.md et applique cette procédure.
```

---

# 40. Tableau comparatif final

| Besoin                   | Claude Code officiel               | OpenClaude dans ce TP                    |
| ------------------------ | ---------------------------------- | ---------------------------------------- |
| Lancer l’outil           | `claude`                           | `openclaude`                             |
| Modèle utilisé           | Claude                             | Ollama ou autre fournisseur              |
| Coût                     | selon l’offre Anthropic            | gratuit avec modèle local                |
| Initialiser le projet    | `/init`                            | création manuelle de `CLAUDE.md`         |
| Voir l’aide              | `/help`                            | `/help` si disponible                    |
| Choisir fournisseur      | généralement non nécessaire        | `/provider` ou variables d’environnement |
| Voir les modifications   | `/diff`                            | `git diff` recommandé                    |
| Gérer le contexte        | `/compact`, `/context`, `/clear`   | `/clear` si disponible, sinon relancer   |
| Commandes personnalisées | skills dans `.claude/skills/`      | procédures Markdown dans `procedures/`   |
| Fiabilité                | plus élevée                        | dépend du modèle et de la version        |
| Adapté à un TP gratuit   | possible mais pas toujours gratuit | oui avec Ollama                          |

---

# 41. Phrase importante à retenir

La phrase la plus importante de ce TP est :

```text
Un assistant de code ne remplace pas la méthode.
Il amplifie une bonne méthode.
```

La bonne méthode est :

```text
1. Donner un contexte clair
2. Demander un plan
3. Générer une petite modification
4. Vérifier le code
5. Tester
6. Corriger
7. Versionner avec Git
```

OpenClaude est intéressant parce qu’il permet d’apprendre gratuitement un workflow proche de Claude Code, surtout avec Ollama. Mais il faut comprendre que ce n’est pas exactement Claude Code officiel.

Donc, dans ce TP, nous utilisons OpenClaude de façon prudente et professionnelle :

```text
CLAUDE.md pour les règles
prompts explicites pour les plans
Git pour vérifier les changements
procedures/ pour remplacer les slash commands personnalisées
tests manuels pour valider l’application
```

C’est exactement ce qu’il faut enseigner à des étudiants débutants : non seulement coder, mais apprendre à travailler proprement avec l’IA.

[1]: https://github.com/Gitlawb/openclaude?utm_source=chatgpt.com "Gitlawb/openclaude: runs anywhere. uses anything"
[2]: https://code.claude.com/docs/en/commands?utm_source=chatgpt.com "Commands - Claude Code Docs"
[3]: https://code.claude.com/docs/en/skills?utm_source=chatgpt.com "Extend Claude with skills - Claude Code Docs"
