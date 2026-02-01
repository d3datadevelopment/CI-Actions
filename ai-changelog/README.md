# AI Changelog Generator – GitHub Action

**AI Changelog Generator** ist eine **Composite GitHub Action**, die automatisch einen **Keep a Changelog**-konformen *Unreleased*-Eintrag erzeugt und in eine bestehende `CHANGELOG.md` integriert.

Die Action kombiniert:

* **git** zur Ermittlung relevanter Commit Messages seit dem letzten Release-Tag
* **ChatGPT (OpenAI API)** zur semantischen Analyse und Strukturierung der Änderungen
* **awk** zur deterministischen Aktualisierung des `Unreleased`-Blocks
* **git push** zur Rückschreibung ins Repository

Zielgruppe sind **Entwickler, Agenturen und Maintainer**, die konsistente, technisch saubere Changelogs mit **wenig** manueller Pflege erzeugen möchten.

Die KI erzeugt **ausschließlich den Body** des *Unreleased*-Abschnitts.

## Zweck & Funktionsweise

1. Ermittelt den letzten Release-Tag (`*.*.*.*`) auf dem aktuellen Branch (first-parent).
2. Sammelt alle Commit Messages zwischen letztem Tag und `HEAD`.
3. Übergibt diese Commits an die OpenAI API mit einem strikt definierten Prompt.
4. Erzeugt daraus den **Body** eines Keep-a-Changelog-konformen *Unreleased*-Blocks.
5. Baut einen vollständigen `## [Unreleased]`-Block inkl. Compare-Link.
6. Ersetzt einen bestehenden *Unreleased*-Block vollständig (AI-managed).
7. Committet und pusht die aktualisierte `CHANGELOG.md`.

## Voraussetzungen

* Repository mit bestehender `CHANGELOG.md`
* Git-Tags nach dem Schema `MAJOR.MINOR.PATCH.BUILD` (z. B. `1.4.2.0`)
* Python ≥ 3.x im Runner
* Gültiger OpenAI API Key
* Push-Token mit Schreibrechten auf das Ziel-Repository

## Inputs

| Name             | Required | Beschreibung                                                            |
| ---------------- | -------- | ----------------------------------------------------------------------- |
| `openai_api_key` | ja       | OpenAI API Key zur Generierung der Changelog-Einträge                   |
| `repo_url`       | ja       | Basis-URL des Repositories (z. B. `https://git.example.com/OWNER/REPO`) |
| `push_token`     | ja       | Token mit Push-Rechten für das Ziel-Repository                          |

## Integrationsbeispiel

```yaml
- name: Generate AI changelog
  uses: your-org/ai-changelog-generator@v1
  with:
    openai_api_key: ${{ secrets.OPENAI_API_KEY }}
    repo_url: https://git.example.com/myorg/myrepo
    push_token: ${{ secrets.REPO_PUSH_TOKEN }}
```
