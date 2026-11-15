# TP5 – Travail collaboratif avec Git et GitHub

**Filière :** Développement Informatique
**Réalisé par :** Khadija YASSINE ([@yassinekhadija63-png](https://github.com/yassinekhadija63-png)) et Douaa NIDBENALI ([@douaaNid](https://github.com/douaaNid))

---

## 1. Introduction

Ce TP a pour objectif d'apprendre à travailler à plusieurs sur un même projet grâce à Git et GitHub. Il ne s'agit pas de développer une application complexe, mais de pratiquer les mécanismes du travail collaboratif : dépôt commun, branches, commits, Pull Requests, fusions et résolution de conflits.

Le principe général suivi est le suivant : une branche personnelle, puis une Pull Request vers la branche `dev`, puis une Pull Request finale de `dev` vers `main`.

## 2. Objectifs du TP

1. Créer un dépôt GitHub commun et y ajouter les collaborateurs.
2. Utiliser les branches `main` (version stable) et `dev` (intégration).
3. Créer des branches `feature/...` pour chaque fonctionnalité.
4. Utiliser les commandes `git add`, `git commit`, `git push` et `git pull`.
5. Créer et fusionner des Pull Requests.
6. Provoquer puis résoudre un conflit Git simple.

## 3. Présentation du projet

### 3.1 Thème choisi

Une petite application frontend intitulée **« Liste de produits »**. Elle permet d'afficher une liste de produits et propose une zone de recherche ainsi qu'un filtre.

### 3.2 Structure du projet

```text
tp5/
├── index.html
├── style.css
└── script.js
```

### 3.3 Équipe et dépôt

Le projet est réalisé en binôme par Khadija YASSINE (compte GitHub `yassinekhadija63-png`) et Douaa NIDBENALI (compte GitHub `douaaNid`). Le dépôt public se nomme `tp5` et appartient à `douaaNid`. Khadija y a été ajoutée comme collaboratrice.

## 4. Répartition du travail

Comme il s'agit d'un binôme, le projet comporte deux fonctionnalités différentes, chacune prise en charge par un membre du groupe :

| Fonctionnalité | Branche | Réalisée par |
|---|---|---|
| Recherche (zone de recherche dans `index.html` et `script.js`) | `feature/recherche` | Douaa NIDBENALI |
| Filtre | `feature/filtre` | Khadija YASSINE |

Une branche `feature/base` a également servi à poser la première version du projet. Chaque branche a été créée à partir de `dev`, afin que le travail de chacun reste isolé jusqu'à son intégration.

## 5. Déroulement du TP

### 5.1 Création du dépôt et des branches

Douaa a créé le dépôt GitHub public, puis a ajouté Khadija comme collaboratrice. Le groupe utilise la branche `main` comme version stable et la branche `dev` comme branche d'intégration. Chaque membre a cloné le projet avec les commandes suivantes :

```bash
git clone URL_DU_DEPOT
git checkout dev
git pull
```

### 5.2 Travail sur les branches de fonctionnalités

Chaque membre a créé sa branche depuis `dev`, puis a travaillé selon le cycle suivant :

```bash
git checkout -b feature/nom-fonctionnalite
git status
git add .
git commit -m "Message clair"
git push -u origin feature/nom-fonctionnalite
```

Rôle des commandes :

- `git add` prépare les fichiers modifiés ;
- `git commit` enregistre une version dans l'historique local avec un message explicatif ;
- `git push` envoie les commits vers GitHub ;
- `git pull` récupère les modifications des autres membres.

L'historique montre des commits aux messages explicites, par exemple « la base du project », « Ajouter zone de recherche », « Ajouter filtre » ou « premier version ».

### 5.3 Pull Requests

Une fois une fonctionnalité terminée et envoyée sur GitHub, une Pull Request est créée de la branche `feature` vers `dev`. Avant chaque fusion, nous avons vérifié les fichiers modifiés, les commits et le bon fonctionnement, ainsi que l'absence de suppression du travail de l'autre membre.

Le dépôt contient au total sept Pull Requests :

| PR | Branches | Description |
|---|---|---|
| #1 | `feature/base` → `dev` | Première version du projet |
| #2 | `feature/recherche` → `dev` | Ajout de la zone de recherche |
| #3 | `feature/fitre` → `dev` | Ajout du filtre |
| #4 | `feature/chenge-a` → `dev` | Première modification du conflit |
| #5 et #6 | `feature/change-b` → `dev` | Seconde modification du conflit, après résolution |
| #7 | `dev` → `main` | Fusion finale |

## 6. Exercice obligatoire : création et résolution d'un conflit

### 6.1 Création du conflit

Pour provoquer volontairement un conflit, deux branches ont été créées depuis la même version de `dev` : `feature/chenge-a` (Douaa) et `feature/change-b` (Khadija). Les deux membres ont modifié la même ligne du fichier `index.html`, à savoir le titre de la page :

1. Douaa a écrit le titre « Produits » (branche `feature/chenge-a`).
2. Khadija a écrit le titre « Products » (commit « Update page title Products », branche `feature/change-b`).

La première branche (`feature/chenge-a`) a été fusionnée dans `dev` par la Pull Request #4. Ensuite, en récupérant `dev` dans `feature/change-b` avec la commande `git pull origin dev`, Git a signalé un conflit.

### 6.2 Message de Git

```text
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
```

Dans le fichier `index.html`, VS Code affiche les marqueurs de conflit. La partie `HEAD` (modification actuelle) contient le titre « Products » de la branche `feature/change-b`, et la partie après le signe égal (modification entrante) contient le titre « Produits » venant de `dev`.

### 6.3 Pourquoi le conflit est-il apparu ?

Le conflit est apparu parce que deux membres ont modifié la même ligne du même fichier à partir de la même version de départ. Lors de la fusion, Git a trouvé deux versions différentes au même endroit et ne pouvait pas décider automatiquement laquelle conserver. Il a donc demandé une intervention humaine.

### 6.4 Résolution

Le groupe a analysé les deux versions et choisi le titre final. La résolution a ensuite été enregistrée :

```bash
git add .
git commit -m "Resolve merge conflict"
git push
```

## 7. Fusion finale vers `main`

Lorsque toutes les fonctionnalités ont fonctionné dans `dev`, une dernière Pull Request de `dev` vers `main` a été créée (PR #7). Avant cette fusion, nous avons vérifié :

1. le bon fonctionnement de la recherche ;
2. le bon fonctionnement du filtre ;
3. l'absence de conflit restant ;
4. l'historique des commits, des branches et des Pull Requests.

Le dernier commit sur `main` est « Merge pull request #7 from doaa-ndd/dev ».

## 8. Historique des commits

Le dépôt compte 14 commits, avec des contributions identifiables des deux membres du groupe.

## 9. Résultat obtenu

À la fin du TP, le dépôt GitHub montre bien tous les éléments demandés :

1. la branche `main` et la branche `dev` ;
2. les branches de travail : `feature/recherche`, `feature/fitre`, `feature/chenge-a` et `feature/change-b` ;
3. des commits réalisés par les deux membres ;
4. sept Pull Requests et leurs fusions ;
5. la résolution d'un conflit Git ;
6. la version finale fonctionnelle du projet.

## 10. Conclusion

Ce TP nous a permis de comprendre qu'un projet collaboratif ne consiste pas seulement à partager des fichiers. Chaque membre travaille sur sa propre branche, enregistre son travail, le partage via une Pull Request et l'intègre progressivement dans le projet commun. La résolution du conflit nous a aussi montré comment Git protège le travail de chacun et pourquoi la communication au sein de l'équipe reste essentielle.

**Le schéma à retenir :** une fonctionnalité, une branche, des commits, un push, une Pull Request vers `dev`, puis une Pull Request de `dev` vers `main`.
