# TP — Créer une mini application Python avec Claude Code

Dans ce TP, nous allons créer une petite application graphique en Python avec **Tkinter**.
L’objectif est double :

1. construire une mini application simple ;
2. apprendre à utiliser les **slash commands** de Claude Code.

À la fin du TP, vous saurez utiliser :

```text
/help
/init
/plan
/diff
/context
/compact
/permissions
```

Vous allez aussi créer vos propres commandes personnalisées :

```text
/python-feature
/explain-python
```

---

# 1. Création du dossier du projet

Commencez par ouvrir votre terminal.

Créez un nouveau dossier :

```bash
mkdir mini-app-python-claude
```

Entrez dans ce dossier :

```bash
cd mini-app-python-claude
```

Créez maintenant le fichier principal de l’application :

```bash
touch main.py
```

Sur Windows PowerShell, utilisez plutôt :

```powershell
New-Item main.py
```

À ce stade, votre projet contient simplement un fichier vide :

```text
mini-app-python-claude/
└── main.py
```

---

# 2. Ouverture du projet avec Claude Code

Dans le même dossier, lancez Claude Code :

```bash
claude
```

Vous êtes maintenant dans une session Claude Code.

Claude Code va nous aider à lire, modifier et améliorer notre projet Python.

---

# 3. Première commande : `/help`

Dans Claude Code, tapez :

```text
/help
```

Cette commande permet d’afficher l’aide de Claude Code.

Elle sert à comprendre quelles commandes sont disponibles dans votre environnement.

Retenez ceci :

```text
Les slash commands sont des commandes spéciales qui commencent par /.
Elles servent à contrôler Claude Code.
```

---

# 4. Afficher la liste des commandes disponibles

Tapez simplement :

```text
/
```

Claude Code affiche alors une liste de commandes disponibles.

C’est une bonne habitude à prendre : quand vous ne savez plus quelle commande utiliser, tapez simplement `/`.

---

# 5. Initialiser le projet avec `/init`

Nous allons maintenant initialiser le projet.

Dans Claude Code, tapez :

```text
/init
```

Cette commande crée généralement un fichier important :

```text
CLAUDE.md
```

Ce fichier sert à donner des instructions permanentes à Claude Code pour ce projet.

Maintenant, demandez à Claude Code d’améliorer ce fichier :

```text
Améliore le fichier CLAUDE.md pour ce projet.

Contexte :
- C’est une mini application Python pour étudiants débutants.
- L’application utilise Tkinter.
- Le fichier principal est main.py.
- Le code doit rester simple, lisible et commenté.
- Ne pas utiliser de framework web.
- Ne pas utiliser React.
- Ne pas ajouter de dépendances externes.
- Chaque modification doit être expliquée.
```

---

# 6. Demander un plan avec `/plan`

Avant de demander à Claude Code de coder, nous allons lui demander de réfléchir.

Dans Claude Code, tapez :

```text
/plan créer une mini application Python Tkinter pour gérer une liste de tâches
```

Le but est d’obtenir un plan avant la génération du code.

Un bon plan pourrait ressembler à ceci :

```text
1. Créer une fenêtre Tkinter
2. Ajouter un champ de saisie
3. Ajouter un bouton Ajouter
4. Ajouter une liste pour afficher les tâches
5. Ajouter un bouton pour marquer une tâche comme terminée
6. Ajouter un bouton pour supprimer une tâche
```

C’est une bonne pratique : on ne demande pas directement à l’IA de coder.
On lui demande d’abord un plan.

---

# 7. Créer la première version de l’application

Maintenant, demandez à Claude Code de créer la première version.

Copiez-collez ce message dans Claude Code :

```text
Crée la version 1 de l’application dans main.py.

Contraintes :
- Utilise Python avec Tkinter.
- Crée une seule fenêtre principale.
- Ajoute un champ Entry pour écrire une tâche.
- Ajoute un bouton Ajouter.
- Ajoute une Listbox pour afficher les tâches.
- Ajoute un bouton Marquer comme terminée.
- Ajoute un bouton Supprimer.
- Garde le code simple pour débutants.
- Ajoute des commentaires dans le code.
- Ne crée pas plusieurs fichiers pour l’instant.
```

Claude Code va modifier le fichier :

```text
main.py
```

---

# 8. Vérifier les modifications avec `/diff`

Après la modification, ne lancez pas immédiatement le programme.

Commencez par vérifier ce que Claude Code a changé.

Dans Claude Code, tapez :

```text
/diff
```

Cette commande affiche les modifications faites dans les fichiers.

C’est une étape importante.

Retenez cette règle :

```text
On ne fait jamais confiance aveuglément à une IA.
On vérifie toujours les modifications avec /diff.
```

---

# 9. Tester l’application Python

Dans le terminal, lancez l’application :

```bash
python main.py
```

Sur certains systèmes, utilisez :

```bash
python3 main.py
```

Une fenêtre graphique doit s’ouvrir.

Testez maintenant les actions suivantes :

```text
1. Écrivez une tâche dans le champ.
2. Cliquez sur Ajouter.
3. Sélectionnez la tâche.
4. Cliquez sur Marquer comme terminée.
5. Sélectionnez une tâche.
6. Cliquez sur Supprimer.
```

Si tout fonctionne, vous avez créé votre première mini application Python avec Claude Code.

---

# 10. Code attendu pour `main.py`

Votre fichier peut ressembler à ceci :

```python
import tkinter as tk
from tkinter import messagebox


def ajouter_tache():
    texte = entree_tache.get()

    if texte.strip() == "":
        messagebox.showwarning("Attention", "Veuillez écrire une tâche.")
        return

    liste_taches.insert(tk.END, texte)
    entree_tache.delete(0, tk.END)


def terminer_tache():
    selection = liste_taches.curselection()

    if not selection:
        messagebox.showwarning("Attention", "Veuillez sélectionner une tâche.")
        return

    index = selection[0]
    tache = liste_taches.get(index)

    if not tache.startswith("[Terminée] "):
        liste_taches.delete(index)
        liste_taches.insert(index, "[Terminée] " + tache)


def supprimer_tache():
    selection = liste_taches.curselection()

    if not selection:
        messagebox.showwarning("Attention", "Veuillez sélectionner une tâche.")
        return

    index = selection[0]
    liste_taches.delete(index)


fenetre = tk.Tk()
fenetre.title("Mini Gestionnaire de Tâches")
fenetre.geometry("500x400")

titre = tk.Label(
    fenetre,
    text="Gestionnaire de tâches",
    font=("Arial", 18, "bold")
)
titre.pack(pady=10)

entree_tache = tk.Entry(fenetre, width=40, font=("Arial", 12))
entree_tache.pack(pady=10)

bouton_ajouter = tk.Button(
    fenetre,
    text="Ajouter",
    width=20,
    command=ajouter_tache
)
bouton_ajouter.pack(pady=5)

liste_taches = tk.Listbox(fenetre, width=50, height=10, font=("Arial", 12))
liste_taches.pack(pady=10)

bouton_terminer = tk.Button(
    fenetre,
    text="Marquer comme terminée",
    width=25,
    command=terminer_tache
)
bouton_terminer.pack(pady=5)

bouton_supprimer = tk.Button(
    fenetre,
    text="Supprimer",
    width=25,
    command=supprimer_tache
)
bouton_supprimer.pack(pady=5)

fenetre.mainloop()
```

---

# 11. Ajouter une amélioration avec `/plan`

Nous allons maintenant améliorer l’application.

Objectif : sauvegarder les tâches dans un fichier JSON.

Dans Claude Code, tapez :

```text
/plan ajouter une sauvegarde des tâches dans un fichier JSON
```

Attendez que Claude Code propose un plan.

Ensuite, demandez :

```text
Ajoute une sauvegarde automatique des tâches dans un fichier tasks.json.

Contraintes :
- Quand on ajoute une tâche, elle est sauvegardée.
- Quand on supprime une tâche, le fichier est mis à jour.
- Quand on ouvre l’application, les tâches existantes sont chargées.
- Garde le code simple pour débutants.
- Explique les changements.
```

---

# 12. Vérifier encore avec `/diff`

Après cette amélioration, tapez encore :

```text
/diff
```

Observez les changements.

Claude Code devrait avoir ajouté des éléments comme :

```text
import json
sauvegarder_taches()
charger_taches()
tasks.json
```

---

# 13. Surveiller le contexte avec `/context`

Après plusieurs échanges avec Claude Code, tapez :

```text
/context
```

Cette commande permet de voir l’utilisation du contexte.

Plus une conversation est longue, plus Claude Code garde d’informations en mémoire.
La commande `/context` permet de vérifier si la session devient trop lourde.

---

# 14. Résumer la session avec `/compact`

Quand la session devient longue, tapez :

```text
/compact Garde seulement l’état actuel du projet, les fichiers modifiés, les décisions importantes et les prochaines étapes.
```

Cette commande permet de résumer la conversation et de continuer plus proprement.

Retenez ceci :

```text
/context permet de voir l’état du contexte.
/compact permet de le résumer pour continuer plus efficacement.
```

---

# 15. Contrôler les permissions avec `/permissions`

Dans Claude Code, tapez :

```text
/permissions
```

Cette commande permet de contrôler ce que Claude Code peut faire.

Par exemple :

```text
- lire des fichiers
- modifier des fichiers
- exécuter certaines commandes
```

C’est important, parce que Claude Code peut agir directement sur votre projet.

---

# 16. Créer une commande personnalisée : `/python-feature`

Nous allons maintenant créer notre propre slash command.

Elle servira à ajouter une fonctionnalité Python proprement.

Dans le terminal, créez le dossier :

```bash
mkdir -p .claude/skills/python-feature
```

Créez ensuite ce fichier :

```bash
nano .claude/skills/python-feature/SKILL.md
```

Sur Windows, créez manuellement ce fichier dans VS Code :

```text
.claude/skills/python-feature/SKILL.md
```

Ajoutez ce contenu :

```markdown
---
description: Ajoute une fonctionnalité Python simple dans une application Tkinter pour étudiants débutants.
---

Tu dois ajouter une fonctionnalité à une application Python Tkinter.

Demande de l’utilisateur :

$ARGUMENTS

Méthode obligatoire :

1. Lire le fichier main.py.
2. Proposer un mini-plan simple.
3. Modifier le code avec prudence.
4. Garder le code compréhensible pour des débutants.
5. Ne pas ajouter de dépendance externe.
6. Ajouter des commentaires pédagogiques.
7. Expliquer les changements à la fin.
8. Donner la commande pour tester l’application.
```

Maintenant, dans Claude Code, utilisez votre commande :

```text
/python-feature ajouter un bouton qui efface toutes les tâches
```

Claude Code va comprendre que `/python-feature` est une commande personnalisée.

---

# 17. Créer une commande personnalisée : `/explain-python`

Nous allons créer une deuxième commande.

Elle servira à expliquer du code Python ligne par ligne.

Créez le dossier :

```bash
mkdir -p .claude/skills/explain-python
```

Créez le fichier :

```bash
nano .claude/skills/explain-python/SKILL.md
```

Ajoutez ce contenu :

```markdown
---
description: Explique du code Python ligne par ligne pour des étudiants débutants.
---

Explique le code demandé de manière très pédagogique.

Code ou fichier à expliquer :

$ARGUMENTS

Structure obligatoire :

1. Rôle général du code.
2. Explication des imports.
3. Explication des variables importantes.
4. Explication des fonctions.
5. Explication des événements Tkinter.
6. Erreurs fréquentes à éviter.
7. Résumé final très simple.
```

Utilisez ensuite la commande :

```text
/explain-python main.py
```

---

# 18. Résumé final

Dans ce TP, vous avez appris à utiliser Claude Code pour construire une application Python simple.

Vous avez utilisé les commandes suivantes :

```text
/help
```

Afficher l’aide.

```text
/
```

Voir les commandes disponibles.

```text
/init
```

Initialiser le projet avec `CLAUDE.md`.

```text
/plan
```

Demander un plan avant de coder.

```text
/diff
```

Vérifier les modifications.

```text
/context
```

Voir l’utilisation du contexte.

```text
/compact
```

Résumer une longue session.

```text
/permissions
```

Contrôler ce que Claude Code peut faire.

Vous avez aussi créé deux commandes personnalisées :

```text
/python-feature
/explain-python
```

L’idée essentielle à retenir est simple :

```text
Claude Code ne sert pas seulement à générer du code.
Il sert à piloter un vrai processus de développement :
planifier, coder, vérifier, améliorer et expliquer.
```


[1]: https://code.claude.com/docs/en/commands "Commands - Claude Code Docs"
[2]: https://code.claude.com/docs/en/permissions "Configure permissions - Claude Code Docs"
[3]: https://code.claude.com/docs/en/skills "Extend Claude with skills - Claude Code Docs"
