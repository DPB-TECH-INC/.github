# .github

Fichiers communs de l'organisation DPB Tech. GitHub les applique automatiquement à tous les dépôts de l'organisation qui n'ont pas les leurs.

## Contenu

| Fichier | Rôle |
|---|---|
| `.github/ISSUE_TEMPLATE/task.yml` | Formulaire de tâche : Context, What to do, Acceptance criteria, Dependencies |
| `.github/ISSUE_TEMPLATE/bug.yml` | Formulaire de bogue : étapes pour reproduire, résultat obtenu et attendu |
| `.github/ISSUE_TEMPLATE/config.yml` | Désactive les issues vides |
| `.github/PULL_REQUEST_TEMPLATE.md` | Modèle de pull request, avec le lien vers l'issue en tête |
| `.github/workflows/pr-checks.yml` | Workflow réutilisable de contrôle des pull requests |

La priorité et l'estimation (en jours) se renseignent après la création de l'issue, dans les champs de l'organisation.

## Règles de travail

- Une branche par changement, jamais de travail direct sur `main`.
- Une pull request est liée à une issue : `Closes #N` en première ligne de la description.
- Fusion en squash uniquement, après la relecture de deux membres de l'équipe.
- Le titre de la PR est `<numéro de l'issue>: <titre de l'issue>` ; le workflow le renomme automatiquement.

## Utiliser le workflow `pr-checks` dans un dépôt

Le workflow vérifie qu'une issue est liée à la PR (le contrôle passe au rouge sinon) et renomme le titre. Un dépôt qui ne crée pas de pull requests n'a pas besoin de l'appeler.

Ajouter dans le dépôt le fichier `.github/workflows/pr-checks.yml` :

```yaml
name: PR checks

on:
  pull_request:
    types: [opened, edited, reopened, synchronize]

jobs:
  pr-checks:
    permissions:
      contents: read
      pull-requests: write
    uses: DPB-TECH-INC/.github/.github/workflows/pr-checks.yml@main
```

### Issue d'un autre dépôt

Pour une issue transversale, écrire `Closes DPB-TECH-INC/<dépôt>#N`. Le contrôle accepte la référence, mais le titre de la PR doit alors être renommé à la main (`N: titre`), car le workflow ne peut pas lire les issues d'un autre dépôt privé.
