All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased](https://git.d3data.de/D3Public/CI-Actions/compare/v1.1.0...rel_1.x)

## [v1.1.0](https://git.d3data.de/D3Public/CI-Actions/compare/v1.0.0...v1.1.0) - 2026-02-04

### Added
- don't block insecure composer packages
- run install wizard script if available
- install dev-dependencies from plugin composer definition
- add allow Composer plugins task
- add PHPStan task to composer test runner and oxid test runner if a configuration file is present

### Changed
- can use comma separated list for modules to be activated
- check for PHPUnit configuration file, otherwise skip test run
- use RFC2606 compatible test mail address

### Fixed

## [v1.0.0](https://git.d3data.de/D3Public/CI-Actions/release/v1.0.0) - 2025-12-26

### Added
- add initial OXID plugin test action (composite)
- add clear tmp task to OXID runner to regnerate DI container
- make module id optional for services only plugins
- add testtools library for OXID plugin tests
- add syntax checks for OXID plugin test