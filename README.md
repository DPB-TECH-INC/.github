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
| `workflow-templates/pr-checks.yml` | Modèle de workflow : appel de `pr-checks` proposé dans l'onglet Actions de chaque dépôt |

La priorité et l'estimation (en jours) se renseignent après la création de l'issue, dans les champs de l'organisation.

## Règles de travail

- Une branche par changement, jamais de travail direct sur `main`.
- Une pull request est liée à une issue : `Closes #N` en première ligne de la description.
- Fusion en squash uniquement, après la relecture de deux membres de l'équipe.
- Le titre de la PR suit la [nomenclature](#titre-de-la-pr) ci-dessous ; le workflow le renomme automatiquement pour une issue du même dépôt.

## Utiliser le workflow `pr-checks` dans un dépôt

Le workflow vérifie qu'une issue est liée à la PR (le contrôle passe au rouge sinon) et renomme le titre. Un dépôt qui ne crée pas de pull requests n'a pas besoin de l'appeler.

**Voie rapide :** dans le dépôt, onglet **Actions** → **New workflow** → section de l'organisation → **PR checks (DPB Tech)** → **Configure** → **Commit**.

**À la main :** ajouter dans le dépôt le fichier `.github/workflows/pr-checks.yml` :

```yaml
name: PR checks

on:
  pull_request:
    types: [opened, edited, reopened, synchronize]

jobs:
  pr-checks:
    permissions:
      contents: read
      issues: read
      pull-requests: write
    uses: DPB-TECH-INC/.github/.github/workflows/pr-checks.yml@main
```

Le droit `issues: read` est nécessaire : sans lui, le jeton du workflow ne voit pas les issues d'un dépôt privé et le contrôle échoue à tort (« This PR must be linked to an issue »), même quand le lien existe.

### Issue d'un autre dépôt

Pour une issue transversale, écrire `Closes DPB-TECH-INC/<dépôt>#N`. Le contrôle accepte la référence, mais le titre de la PR doit alors être renommé à la main (voir [Titre de la PR](#titre-de-la-pr)), car le workflow ne peut pas lire les issues d'un autre dépôt privé.

## Titre de la PR

La numérotation est propre à chaque dépôt : `operations#12` et `site-web#12` sont deux issues différentes. Le titre de la PR dit donc de quelle issue il s'agit sans ambiguïté.

| L'issue est… | Forme du titre | Exemple |
|---|---|---|
| Dans le **même dépôt** que la PR | `<numéro>: <titre de l'issue>` | `12: Page « Contact » sur le site` |
| Dans **un autre dépôt** | `<dépôt>#<numéro>: <titre de l'issue>` | `operations#12: Page LinkedIn de DPB Tech` |

Le premier cas est renommé automatiquement. Le second se renomme à la main.

Dans une conversation ou un message, nomme aussi le dépôt avec le numéro (`operations#12`), pour ne pas confondre deux issues qui portent le même numéro.
