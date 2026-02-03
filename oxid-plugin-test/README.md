# OXID Plugin Test – Reproduzierbare CI-Tests für OXID-Module

Kategorie: CI

**OXID Plugin Test** ist eine umfangreiche Composite GitHub Action zur automatisierten Qualitätssicherung von **OXID eShop Modulen** in einer realistischen Shop-Umgebung.
Sie bildet einen vollständigen OXID-Installations- und Testlauf nach und eignet sich damit besonders für **Agenturen, Modulhersteller und Enterprise-Setups**, die Plugins versions- und PHP-abhängig absichern müssen.

Im Gegensatz zu reinen Paket-Tests wird hier bewusst **gegen einen echten OXID Shop** getestet – inklusive Setup, Modulinstallation, Aktivierung und optionaler SourceGuardian-Unterstützung.

## Typische Einsatzszenarien

* Qualitätssicherung von OXID-Modulen über mehrere Shop-Versionen hinweg
* CI-Matrix für PHP- und OXID-Kompatibilität
* Agentur-Standards für Kunden-Plugins
* Vorbereitung von Releases und zertifizierten Modul-Versionen
* Tests von SourceGuardian-geschützten Modulen

## Abgedeckter Workflow

**1. PHP- & Runtime-Setup**

* Frei wählbare PHP-Version
* Relevante Extensions für OXID (`mbstring`, `intl`, `gd`, `mysql`, …)
* Speicher- und Zeitzonenanpassung für CI-Umgebungen
* Optional: Installation & Aktivierung des **SourceGuardian Loaders**

---

**2. Optionale PHP-Syntaxprüfung**

* Rekursive `php -l`-Checks auf konfigurierbaren Pfaden
* Mehrere Pfade via Komma-Liste
* Ideal für Modul-Code vor Shop-Integration

---

**3. OXID Shop Installation**

* Installation einer definierten OXID-Version oder eines Branches (`oxid_ref`)
* Vollständiges Shop-Setup via `oe-console`
* Datenbankanbindung über CI-Environment-Variablen
* Anlage eines Admin-Users
* Automatische Theme-Aktivierung, sofern unterstützt

---

**4. Modul-Integration**

* Registrierung des Modul-Repositories per Composer (`path`-Repository)
* Installation des Plugins über den angegebenen Composer-Paketnamen
* Optionale Modul-Aktivierung über die OXID Modul-IDs
* Bereinigung des TMP-Verzeichnisses vor Tests

---

**5. Statische Analyse (PHPStan, optional)**

* Automatische Ausführung bei vorhandener PHPStan-Konfiguration
* Bevorzugt Konfiguration aus dem Plugin selbst
* Debug-Modus mit vollständigem Analyse-Output
* Fehler schlagen den Build fehl

---

**6. PHPUnit-Tests**

* Installation einer frei wählbaren PHPUnit-Version
* Unterstützung für OXID-spezifische Test-Tooling (`d3/testingtools`)
* Tests laufen **innerhalb des Shop-Kontexts**
* Unterstützung für:

  * komplette Testläufe
  * gezielte Test-Suites
* Aktivierte Qualitäts-Guards:

  * `--fail-on-risky`
  * `--fail-on-warning`

## Anforderungen

* mindestens OXID eShop 7.0
* vollständige Unterstützung ab OXID eShop 7.1

## Inputs

| Name                  | Typ    | Pflicht | Beschreibung                                        | Beispiel              |
|-----------------------|--------|---------|-----------------------------------------------------|-----------------------|
| php_version           | string | ja      | PHP-Version                                         | "8.0"                 |
| oxid_ref              | string | ja      | OXID Version                                        | "dev-b-7.4-ce"        |
| sourceguardian        | bool   | nein    | SourceGuardian aktivieren                           | "true"                |
| composer_package_name | string | ja      | Composer Package Name                               | "d3/mypackage"        |
| oxid_module_ids       | string | nein    | OXID Module IDs zur Aktivierung, ggf. kommagetrennt | "d3module,d3mymodule" |
| test_suites           | string | nein    | kommagetrennte PHPUnit Suites                       | "unit,integration"    |
| syntax_check_paths    | string | nein    | kommagetrennte Pfade für Syntax-Check               | "src,tests"           |

## Erwartete ENV-Variablen

Diese müssen vom Workflow gesetzt werden:

* DB_HOST
* DB_NAME
* DB_USER
* DB_PASS
* DB_PORT (optional, Default 3306)

## Integrationsbeispiel

```
- name: Run OXID plugin tests
  uses: d3datadevelopment/ci-actions/oxid-plugin-test@v1
  with:
    php_version: "8.2"
    oxid_ref: "dev-b-7.1-ce"
    composer_package_name: "d3/mailconfigchecker"
    oxid_module_ids: "d3mailconfigchecker"
    test_suites: "unit,integration"
    syntax_check_paths: "src,tests"
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