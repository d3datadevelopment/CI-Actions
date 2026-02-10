# Status Reporter – Status an beliebige APIs melden

Kategorie: CI

Der Status Reporter ist eine schlanke Composite GitHub Action zur Übermittlung von CI-Statusinformationen an ein externes, generisches API-Endpoint.
Sie eignet sich insbesondere für Setups, in denen Build- und Deployment-Status nicht (oder nicht ausschließlich) über GitHub Commit Statuses, sondern über eigene Systeme, Dashboards oder Meta-CI-Infrastrukturen verarbeitet werden.

Die Action sendet strukturierte Statusdaten (State, Context, Beschreibung, Ziel-URL) als JSON per HTTP POST an ein konfigurierbares Endpoint und authentifiziert sich dabei über ein Token-basiertes Header-Verfahren.

## Typische Einsatzszenarien

* Zentrale CI/CD-Statusaggregation über mehrere Repositories hinweg
* Anbindung an interne Release-, Monitoring- oder Deployment-Plattformen
* Ersatz oder Ergänzung von GitHub Commit Statuses bei Self-Hosted- oder Multi-SCM-Setups
* Integration in agenturübergreifende Build-Pipelines mit einheitlichem Statusformat

## Technische Eigenschaften

* Composite Action (keine eigene Runtime, keine Side-Effects)
* Shell-basiert (bash), minimaler Overhead
* JSON-Payload wird sauber via jq erzeugt
* Fehler beim Reporting sind nicht build-blockierend (fail-safe by design)
* API-agnostisch: kein GitHub-spezifisches Schema erzwungen

Die konkrete Interpretation der Felder liegt vollständig beim empfangenden System.

## Verhalten im Fehlerfall

Schlägt der API-Request fehl (Netzwerkfehler, HTTP-Status ≠ 2xx), wird der Fehler protokolliert, der Workflow jedoch nicht abgebrochen.
Das macht die Action robust gegenüber temporären API-Ausfällen und geeignet für produktive CI-Pipelines.

## Inputs

| Name            | Typ    | Pflicht | Beschreibung                        | Beispiel                        |
|-----------------|--------|---------|-------------------------------------|---------------------------------|
| status_endpoint | string | ja      | Vollständige API-URL                | "https://example.org/statuses/" |
| auth_token      | string | ja      | Auth-Token (via Repository Secrets) | "abcdef"                        |
| state           | string | ja      | Ausführungsstatus                   | "success", "failure", ...       |
| context         | string | nein    | Status-Kontext                      | "ci/github"                     |
| description     | string | nein    | Beschreibung                        | "CI passed"                     |
| target_url      | string | nein    | Workflow URL mit Build-Details      |                                 |

## Integrationsbeispiel

```
- name: Report CI status
  uses: d3datadevelopment/ci-actions/status-reporter@status-reporter--v1.0.0
  with:
    status_endpoint: https://example.org/statuses/${{ github.sha }}
    auth_token: ${{ secrets.STATUS_TOKEN }}
    state: success
    description: "CI passed"
    target_url: ${{ github.server_url }}/${{ github.repository }}/actions/runs/${{ github.run_id }}
```
