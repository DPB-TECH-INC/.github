# DPB Tech — dépôt `.github` de l'organisation

## Description

Dépôt des fichiers communs de l'organisation GitHub `DPB-TECH-INC` : formulaires d'issues, modèle de pull request et workflow réutilisable de contrôle des PR. GitHub applique les formulaires et le modèle à tous les dépôts qui n'ont pas les leurs.

**Ce dépôt est PUBLIC** : aucun secret, aucun document client, aucune information interne ou confidentielle.

Le dossier local est `dpb-tech-github-org` pour éviter un dossier caché ; le dépôt distant s'appelle bien `.github`.

## Stack

Pas de code applicatif : fichiers YAML (formulaires d'issues, GitHub Actions) et Markdown.

## Contenu actuel (au 2026-11-06)

- `.github/ISSUE_TEMPLATE/` : `task.yml`, `bug.yml`, `config.yml` (issues vides désactivées)
- `.github/PULL_REQUEST_TEMPLATE.md`
- `.github/workflows/pr-checks.yml` : workflow réutilisable (issue liée obligatoire, renommage du titre)
- `README.md`

## Décisions prises (à appliquer)

- **Tout est nommé en anglais** (fichiers, champs, workflows) ; les **descriptions et le contenu écrits par l'équipe sont en français**.
- Champs des issues : Context, What to do, Acceptance criteria, Dependencies ; Priority et Estimate (days) via les champs d'organisation.
- **Fusion en squash seul.** Titre de la PR : `<numéro de l'issue>: <titre de l'issue>`, renommé **automatiquement** par un workflow à partir de l'issue liée ; pour une issue d'un autre dépôt, `<dépôt>#<numéro>: <titre de l'issue>`, écrit à la main (la numérotation est propre à chaque dépôt).
- **Une PR doit être liée à une issue** (`Closes #N`, ou `Closes DPB-TECH-INC/operations#N` pour une issue transversale). Le contrôle passe au rouge sinon.
- Nom de branche : convention recommandée `<numéro>-<résumé>` (générée par le bouton « Create a branch » de l'issue), **non imposée**.
- Organisation en forfait **Free** : GitHub ne peut pas rendre les contrôles obligatoires sur dépôts privés. La règle repose sur les **2 relectures humaines** (le modèle de PR contient la case « issue liée et critères remplis »).
- Mot « associé » interdit dans les issues : écrire « l'équipe ».
- Chaque champ et chaque phrase des issues commence par une majuscule.
- Issues légères : on dit quoi et comment vérifier, jamais comment faire. Une issue = un résultat relisable en une PR. Pas d'issue « parapluie ».

## Conventions

- Aucune branche de travail directement sur `main` : une branche par changement, une PR, relecture par les deux autres membres.
- Aucun push, PR ou fusion sans demande explicite d'un membre de l'équipe.
- Ces fichiers sont d'abord préparés puis validés par l'équipe avant toute généralisation.

## Avancement

- [x] Dépôt créé, 4 fichiers de modèles en place (anglais)
- [x] Renommer `tache.yml` / `bogue.yml` en `task.yml` / `bug.yml` et aligner les champs
- [x] Modèle de PR : lien vers l'issue en tête, case « issue liée et critères d'acceptation remplis »
- [x] Workflow réutilisable `pr-checks.yml` : issue liée (rouge sinon) + renommage automatique du titre (à tester sur une vraie PR)
- [x] README : contenu du dépôt et appel du workflow depuis un autre dépôt
