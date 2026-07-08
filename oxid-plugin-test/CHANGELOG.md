All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased](https://git.d3data.de/D3Public/CI-Actions/compare/php-tests--v1.4.0...rel_1.x)

## [v1.4.0](https://git.d3data.de/D3Public/CI-Actions/compare/php-tests--v1.3.0...php-tests--v1.4.0) - 2026-07-08

### Changed
- Registered optional Composer repositories from the `.github` manifest when present.

## [v1.3.0](https://git.d3data.de/D3Public/CI-Actions/compare/php-tests--v1.2.0...php-tests--v1.3.0) - 2026-06-10

### Changed
- Extended PHPStan and PHPUnit config discovery to search the repository root, `.ci-tools`, and the full plugin as fallback.

## [v1.2.0](https://git.d3data.de/D3Public/CI-Actions/compare/php-tests--v1.1.0...php-tests--v1.2.0) - 2026-05-21

### Changed
- Cleaned up the CI action configuration and related task structure.
- Added task comments to improve readability of the workflow steps.

### Fixed
- Patched OXID exception swallowing in the test workflow.
- Added YAML linting to validate YAML files during CI.
- Replaced non-ASCII characters with ASCII-safe text where required.

## [v1.1.0](https://git.d3data.de/D3Public/CI-Actions/compare/php-tests--v1.0.0...php-tests--v1.1.0) - 2026-02-04

### Added
- don't block insecure composer packages
- run install wizard script if available
- install dev-dependencies from plugin composer definition
- add allow Composer plugins task
- add PHPStan task to composer test runner and oxid test runner if a configuration file is present
- can set license keys for D3 modules

### Changed
- can use comma separated list for modules to be activated
- check for PHPUnit configuration file, otherwise skip test run
- use RFC2606 compatible test mail address

### Fixed

## [v1.0.0](https://git.d3data.de/D3Public/CI-Actions/release/php-tests--v1.0.0) - 2025-12-26

### Added
- add initial OXID plugin test action (composite)
- add clear tmp task to OXID runner to regnerate DI container
- make module id optional for services only plugins
- add testtools library for OXID plugin tests
- add syntax checks for OXID plugin test