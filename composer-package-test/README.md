# Composer Package Test – Standardisierte CI-Tests für Composer-Pakete

Kategorie: CI

Dies ist eine wiederverwendbare Composite GitHub Action zur Durchführung typischer Qualitäts- und Testschritte für **generische PHP-/Composer-Pakete**.
Sie richtet sich an Teams und Agenturen, die **bibliotheksartige Pakete** (Framework-unabhängig oder Framework-nah) mit einem reproduzierbaren, wartbaren CI-Setup absichern wollen.

Die Action deckt bewusst die klassischen Disziplinen ab: Syntaxprüfung, Dependency-Installation, statische Analyse und automatisierte Tests – ohne projekt- oder framework-spezifische Annahmen zu erzwingen.

## Typische Einsatzszenarien

* Qualitätssicherung für interne Shared Libraries
* Open-Source-Pakete mit minimalem CI-Overhead
* Einheitliches Test-Setup über mehrere Kundenprojekte hinweg
* PHP-Versionen-Tests via GitHub Actions Matrix

## Enthaltene Prüfschritte

**1. PHP-Setup**

* Installation einer frei wählbaren PHP-Version
* Composer v2 als Tooling-Baseline
* Geeignet für Matrix-Builds über mehrere PHP-Versionen

---

**2. Optionale PHP-Syntaxprüfung**

* Rekursive `php -l`-Prüfung auf konfigurierbaren Pfaden
* Mehrere Pfade via Komma-Liste möglich
* Bewusst **optional**, um Legacy- oder Partial-Setups nicht zu blockieren

---

**3. Dependency-Installation**

* Standardisiertes `composer install`
* Keine Interaktion, bevorzugt Dist-Packages
* Erwartet ein korrekt gepflegtes `composer.lock`

---

**4. Statische Analyse mit PHPStan (optional)**

* Automatische Ausführung, falls `phpstan.neon` oder `phpstan.neon.dist` vorhanden ist
* Debug-Modus mit vollständigem Raw-Output möglich
* Fehler schlagen den Build fehl, Warnungen werden sauber durchgereicht

---

**5. PHPUnit-Tests (optional)**

* Automatische Erkennung über `phpunit.xml`
* Unterstützung für:

  * vollständige Testläufe
  * gezielte Test-Suites (`unit`, `integration`, ...)
* Aktivierte Qualitäts-Guards:

  * `--fail-on-risky`
  * `--fail-on-warning`
* Keine Coverage-Erzeugung (bewusst CI-schlank gehalten)

## Inputs

| Name               | Typ    | Pflicht | Beschreibung                          | Beispiel           |
|--------------------|--------|---------|---------------------------------------|--------------------|
| php_version        | string | ja      | PHP-Version                           | "8.4"              |
| test_suites        | string | nein    | PHPUnit Testsuites (kommagetrennt)    | "unit,integration" |
| syntax_check_paths | string | nein    | kommagetrennte Pfade für Syntax-Check | "src,tests"        |

## Integrationsbeispiel

```
- name: Run package tests
  uses: d3datadevelopment/ci-actions/composer-package-test@php-tests--v1.1.0
  with:
    php_version: "8.2"
    syntax_check_paths: "src,Tests"
    test_suites: "unit,integration"
```

## Hinweise

### PHPStan

Für CI Runs von OXID Modulen werden diese via Symlink in den Shop eingebunden. Beachten Sie, in Ihrer PHPStan 
Konfiguration alle zu prüfenden (Root-)Ordner und Dateien explizit anzugeben. Globale Angaben (z.B. '.') kann 
durch die Verwendung von Symlinks zu Endlosschleifen führen.

```
parameters:
  paths: 
    - Core
    - ...

  scanFiles:
    - Context.php
    - ...
```
