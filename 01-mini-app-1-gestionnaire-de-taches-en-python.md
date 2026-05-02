# Mini application : Gestionnaire de tâches en Python

Fonctions :

```text
1. Ajouter une tâche
2. Marquer une tâche comme terminée
3. Supprimer une tâche
4. Afficher les tâches dans une liste
```

On va utiliser **Claude Code** pour construire l’application étape par étape avec les slash commands.

Les slash commands sont des commandes qui commencent par `/` dans Claude Code. Tu peux taper simplement `/` pour voir les commandes disponibles, et une commande doit être placée au début du message pour être reconnue. Certaines commandes peuvent varier selon la plateforme, le plan et l’environnement. ([Claude][1])

---

# Étape 1 — Créer le dossier du projet

Dans le terminal :

```bash
mkdir mini-app-python-claude
cd mini-app-python-claude
```

Créer un fichier vide :

```bash
touch main.py
```

Sur Windows PowerShell :

```powershell
New-Item main.py
```

---

# Étape 2 — Ouvrir Claude Code dans ce dossier

Toujours dans le dossier :

```bash
claude
```

Tu arrives dans Claude Code.

---

# Étape 3 — Afficher les commandes disponibles

Dans Claude Code, tape :

```text
/help
```

Cette commande affiche l’aide et les commandes disponibles. La documentation officielle indique aussi que `/help` sert à montrer l’aide et les commandes disponibles. ([Claude][1])

Ensuite tape seulement :

```text
/
```

L’objectif est de montrer aux étudiants que Claude Code propose une liste de commandes.

Tu peux leur dire :

```text
Dans Claude Code, les slash commands servent à contrôler la session.
Ce ne sont pas des commandes Python.
Ce sont des commandes pour piloter Claude Code.
```

---

# Étape 4 — Initialiser le projet avec `/init`

Dans Claude Code :

```text
/init
```

Cette commande initialise le projet avec un fichier `CLAUDE.md`, qui sert de guide pour Claude Code. ([Claude][1])

Ensuite, écris à Claude Code :

```text
Améliore le fichier CLAUDE.md pour ce projet.

Contexte :
- C’est une mini application Python pour étudiants débutants.
- L’application utilise Tkinter.
- Le fichier principal est main.py.
- Le code doit être simple, lisible et commenté.
- Ne pas utiliser de framework web.
- Ne pas utiliser React.
- Ne pas ajouter de dépendances externes.
- Chaque modification doit être expliquée.
```

---

# Étape 5 — Demander un plan avec `/plan`

Avant de coder, on demande à Claude de réfléchir.

Dans Claude Code :

```text
/plan créer une mini application Python Tkinter pour gérer une liste de tâches
```

La commande `/plan` permet d’entrer directement en mode plan avec une description de tâche. ([Claude][1])

Claude devrait proposer quelque chose comme :

```text
1. Créer une fenêtre Tkinter
2. Ajouter un champ de saisie
3. Ajouter un bouton Ajouter
4. Ajouter une liste de tâches
5. Ajouter un bouton Terminer
6. Ajouter un bouton Supprimer
```

Tu expliques aux étudiants :

```text
On ne demande pas directement à l’IA de coder.
On lui demande d’abord un plan.
C’est une bonne pratique professionnelle.
```

---

# Étape 6 — Demander à Claude Code de créer la version 1

Dans Claude Code, écris exactement :

```text
Crée la version 1 de l’application dans main.py.

Contraintes :
- Utilise Python avec Tkinter.
- Une seule fenêtre principale.
- Un champ Entry pour écrire une tâche.
- Un bouton Ajouter.
- Une Listbox pour afficher les tâches.
- Un bouton Marquer comme terminée.
- Un bouton Supprimer.
- Code simple pour débutants.
- Ajoute des commentaires dans le code.
- Ne crée pas plusieurs fichiers pour l’instant.
```

Claude Code va modifier `main.py`.

---

# Étape 7 — Vérifier les changements avec `/diff`

Après la modification, tape :

```text
/diff
```

La commande `/diff` ouvre un visualiseur qui montre les changements non commités et les modifications faites pendant les tours Claude. ([Claude][1])

Phrase importante à dire aux étudiants :

```text
On ne fait jamais confiance aveuglément à l’IA.
On vérifie toujours ce qu’elle a modifié avec /diff.
```

---

# Étape 8 — Tester l’application

Quitte ou garde Claude Code ouvert, puis dans le terminal normal :

```bash
python main.py
```

Sur certains systèmes :

```bash
python3 main.py
```

Une fenêtre doit s’ouvrir.

Teste :

```text
1. Écrire : Acheter du lait
2. Cliquer sur Ajouter
3. Sélectionner la tâche
4. Cliquer sur Marquer comme terminée
5. Cliquer sur Supprimer
```

---

# Code attendu pour main.py

Voici une version simple que Claude Code pourrait produire :

```python
import tkinter as tk
from tkinter import messagebox


# Fonction pour ajouter une tâche
def ajouter_tache():
    texte = entree_tache.get()

    if texte.strip() == "":
        messagebox.showwarning("Attention", "Veuillez écrire une tâche.")
        return

    liste_taches.insert(tk.END, texte)
    entree_tache.delete(0, tk.END)


# Fonction pour marquer une tâche comme terminée
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


# Fonction pour supprimer une tâche
def supprimer_tache():
    selection = liste_taches.curselection()

    if not selection:
        messagebox.showwarning("Attention", "Veuillez sélectionner une tâche.")
        return

    index = selection[0]
    liste_taches.delete(index)


# Création de la fenêtre principale
fenetre = tk.Tk()
fenetre.title("Mini Gestionnaire de Tâches")
fenetre.geometry("500x400")

# Titre
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
    width=20,
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

# Lancement de l'application
fenetre.mainloop()
```

---

# Étape 9 — Demander une amélioration avec `/plan`

Maintenant, on ajoute une amélioration : sauvegarder les tâches dans un fichier.

Dans Claude Code :

```text
/plan ajouter une sauvegarde des tâches dans un fichier JSON
```

Puis :

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

# Étape 10 — Vérifier encore avec `/diff`

Après modification :

```text
/diff
```

Tu montres aux étudiants :

```text
Claude a probablement ajouté :
- import json
- une fonction sauvegarder_taches()
- une fonction charger_taches()
- un fichier tasks.json
```

---

# Étape 11 — Utiliser `/context`

Après plusieurs échanges :

```text
/context
```

La commande `/context` permet de visualiser l’utilisation du contexte et donne des suggestions d’optimisation. ([Claude][1])

Explication simple :

```text
Plus la conversation devient longue, plus Claude garde beaucoup d’informations.
La commande /context permet de voir si la session devient lourde.
```

---

# Étape 12 — Utiliser `/compact`

Quand la conversation devient longue :

```text
/compact Garde seulement l’état actuel du projet, les fichiers modifiés, les décisions importantes et les prochaines étapes.
```

La commande `/compact` libère du contexte en résumant la conversation, avec des instructions optionnelles. ([Claude][1])

Explication aux étudiants :

```text
/compact permet de nettoyer la conversation sans perdre l’essentiel.
```

---

# Étape 13 — Montrer `/permissions`

Dans Claude Code :

```text
/permissions
```

Cette commande permet de gérer les règles d’autorisation, de demande de confirmation et de refus pour les outils utilisés par Claude Code. ([Claude][2])

Tu peux dire :

```text
Claude Code peut lire des fichiers, modifier du code et exécuter certaines commandes.
Donc il faut contrôler ce qu’il a le droit de faire.
```

---

# Étape 14 — Créer une slash command personnalisée pour Python

Maintenant, on crée notre propre commande :

```text
/python-feature
```

Elle servira à ajouter une fonctionnalité Python proprement.

Dans le terminal :

```bash
mkdir -p .claude/skills/python-feature
```

Créer le fichier :

```bash
nano .claude/skills/python-feature/SKILL.md
```

Sur Windows, tu peux créer le fichier manuellement dans VS Code :

```text
.claude/skills/python-feature/SKILL.md
```

Contenu du fichier :

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

Les skills Claude Code se créent avec un fichier `SKILL.md`, et le nom du dossier peut devenir une commande slash invocable directement, par exemple `/python-feature`. ([Claude][3])

Ensuite, dans Claude Code :

```text
/python-feature ajouter un bouton qui efface toutes les tâches
```

---

# Étape 15 — Créer une deuxième commande personnalisée : `/explain-python`

Créer le dossier :

```bash
mkdir -p .claude/skills/explain-python
```

Créer :

```bash
nano .claude/skills/explain-python/SKILL.md
```

Contenu :

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

Utilisation :

```text
/explain-python main.py
```

---

# Étape 16 — Résumé du TP pour tes étudiants

À la fin, les étudiants doivent connaître ces commandes :

```text
/help
```

Voir l’aide.

```text
/
```

Voir les commandes disponibles.

```text
/init
```

Créer le guide du projet `CLAUDE.md`.

```text
/plan
```

Demander un plan avant de coder.

```text
/diff
```

Vérifier les modifications faites par Claude.

```text
/context
```

Voir l’utilisation du contexte.

```text
/compact
```

Résumer la conversation pour continuer proprement.

```text
/permissions
```

Contrôler les droits de Claude Code.

```text
/python-feature
```

Commande personnalisée pour ajouter une fonctionnalité Python.

```text
/explain-python
```

Commande personnalisée pour expliquer du code Python.

---

# Version orale simple pour ton cours

Tu peux présenter ça comme ça :

```text
Aujourd’hui, on ne va pas juste coder une application Python.
On va apprendre à travailler avec Claude Code comme un assistant de développement.

On va utiliser :
/init pour préparer le projet,
/plan pour réfléchir avant de coder,
/diff pour vérifier les changements,
/context pour surveiller la mémoire de la session,
/compact pour résumer quand la conversation devient longue,
/permissions pour contrôler ce que Claude peut faire.

Puis on va créer nos propres commandes :
/python-feature pour ajouter une fonctionnalité,
/explain-python pour expliquer le code.
```


[1]: https://code.claude.com/docs/en/commands "Commands - Claude Code Docs"
[2]: https://code.claude.com/docs/en/permissions "Configure permissions - Claude Code Docs"
[3]: https://code.claude.com/docs/en/skills "Extend Claude with skills - Claude Code Docs"
