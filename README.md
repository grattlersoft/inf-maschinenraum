# Maschinenraum

_Worf 9 Mr. Warp! Sorry Chief, falscher Kanal!_

> CI/CD Infrastruktur, Shared Workflows und Dependabot-Vorlagen für grattlersoft.

[![License: OHNE](https://img.shields.io/badge/License-OHNE-yellow.svg)](LICENSE)

Zentrale Sammlung wiederverwendbarer GitHub-Actions-Workflows und Templates. Consumer-Repos rufen die Reusable Workflows per `uses:` auf; die Dependabot-Vorlage wird beim Repo-Setup kopiert.

## Inhalt

### Reusable Workflows

| Workflow | Für | Inputs |
|----------|-----|--------|
| `reusable-dotnet-ci.yml` | .NET Build + Test | `solution`, `dotnet-version` |
| `reusable-dotnet-release.yml` | .NET Release bei Tag | `solution`, `publish-project`, `dotnet-version` |
| `reusable-vsix-ci.yml` | VS Extension Build + Test | `solution`, `test-dll` |
| `reusable-vsix-release.yml` | VSIX Release bei Tag | `solution`, `vsix-glob` |

### Dependabot

| Datei | Zweck |
|-------|-------|
| `dependabot/dependabot-nuget.yml` | Template: NuGet + GitHub Actions, gebündelt, 1 PR |
| `.github/workflows/cleanup-dependabot.yml` | Schließt alte Dependabot-PRs täglich vor neuem Run |

Prinzip: Daily Check, max 1 PR offen. Cleanup-Job schließt alte PRs täglich um 01:50 UTC. Dependabot erstellt danach einen neuen, aktuellen PR. Kein PR-Müll.

## Verwendung

Consumer-Repos rufen Reusable Workflows per `uses:` auf:

```yaml
jobs:
  ci:
    uses: grattlersoft/inf-maschinenraum/.github/workflows/reusable-dotnet-ci.yml@main
    with:
      solution: src/Projektname.slnx
```

Dependabot-Setup in neuem Repo:

1. `dependabot/dependabot-nuget.yml` nach `.github/dependabot.yml` kopieren
2. `target-branch` anpassen (main oder develop)
3. `cleanup-dependabot.yml` wird aus inf-maschinenraum direkt verwendet (kein Kopieren nötig)

## Lizenz

[OHNE-Lizenz](LICENSE) — Mach was du willst. Wir waren's nicht.
