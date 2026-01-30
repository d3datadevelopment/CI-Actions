# D3 CI Composite Actions

Zentrale Sammlung wiederverwendbarer GitHub Composite Actions

Ziel dieses Repositories ist es, CI-Logik zu standardisieren, Copy-Paste zu vermeiden und Workflows in Projekt-Repositories schlank zu halten.

## Grundprinzipien

Dieses Repository enthält nur Actions, keine Projekt-Pipelines. Die Actions sind bewusst klein, fokussiert und generisch konzipiert. Infrastruktur, 
Secrets und Matrix-Logik sollen bitte im verwendenden Projekt definiert werden. Jeder Ordner enthält genau eine Composite Action.

## Versionierung

Dieses Repository verwendet semantische Versionierung über Git-Tags.

Empfohlene Nutzung in Projekten:

```
uses: d3datadevelopment/ci-actions/<action-name>@v1
```

`v1` zeigt immer auf die aktuelle stabile Version der Major-Reihe. In `rel_X.x` befindet sich die aktuellste Pre-Release Version.

## Enthaltene Actions

* composer-package-test-runner

Dies ist eine wiederverwendbare Composite GitHub Action zur Durchführung typischer Qualitäts- und Testschritte für **generische PHP-/Composer-Pakete**.
Sie richtet sich an Teams und Agenturen, die **bibliotheksartige Pakete** (Framework-unabhängig oder Framework-nah) mit einem reproduzierbaren, wartbaren CI-Setup absichern wollen.

Weitere Infos [hier](./composer-package-test/README.md).

---

* oxid-test-runner

**OXID Plugin Test** ist eine umfangreiche Composite GitHub Action zur automatisierten Qualitätssicherung von **OXID eShop Modulen** in einer realistischen Shop-Umgebung.
Sie bildet einen vollständigen OXID-Installations- und Testlauf nach und eignet sich damit besonders für **Agenturen, Modulhersteller und Enterprise-Setups**, die Plugins versions- und PHP-abhängig absichern müssen.

Weitere Infos [hier](./oxid-plugin-test/README.md).

---

* commit-status-reporter – Status an beliebige APIs melden

Der Status Reporter ist eine schlanke Composite GitHub Action zur Übermittlung von CI-Statusinformationen an ein externes, generisches API-Endpoint.
Sie eignet sich insbesondere für Setups, in denen Build- und Deployment-Status nicht (oder nicht ausschließlich) über GitHub Commit Statuses, sondern über eigene Systeme, Dashboards oder Meta-CI-Infrastrukturen verarbeitet werden.

Weitere Infos [hier](./status-reporter/README.md).

### build-docs - HTML-Dokumentation aus Markdown erzeugen

**Build MkDocs Documentation** ist eine schlanke Composite GitHub Action zum **Erzeugen statischer HTML-Dokumentation** auf Basis von Markdown-Dateien mit **MkDocs und dem Material Theme**.
Sie ist bewusst auf den **Build-Schritt** fokussiert und eignet sich als Baustein in mehrstufigen CI-Pipelines, z. B. in Kombination mit separaten Publish- oder Deploy-Actions.

Weitere Infos [hier](./build-docs/README.md).

### publish-docs - versionierte Dokumentation aus CI heraus deployen

**Publish Documentation** ist eine Composite GitHub Action zur **kontrollierten Veröffentlichung versionierter Dokumentation** in ein separates GitHub-Pages-Repository.
Sie ist dafür gedacht, **bereits generierte Dokumentation** (z. B. aus MkDocs, Docusaurus, Sphinx, Custom-Generatoren) aus einem CI-Workflow heraus **strukturiert, reproduzierbar und versionssicher** zu publizieren.

Weitere Infos [hier](./publish-docs/README.md).

## Beispiele

Schaue in [CI Tests](https://github.com/d3datadevelopment/CI-Tests) für Integrationsbeispiele.

## Selbsttests

Dieses Repository enthält Workflows, die die Aktionen selbst testen.
Die Tests werden anhand externer Test-Repositorys durchgeführt, die echten, ausführbaren Code enthalten.

Diese Workflows werden automatisch ausgelöst, wenn Änderungen an den entsprechenden Aktionsverzeichnissen vorgenommen werden.