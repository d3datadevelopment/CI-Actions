All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased](https://git.d3data.de/D3Public/CI-Actions/compare/v1.1.0...rel_1.x)

## [v1.1.0](https://git.d3data.de/D3Public/CI-Actions/compare/v1.0.0...v1.1.0) - 2026-02-04

### Added
- add PHPStan task to composer test runner and oxid test runner if a configuration file is present
- don't use quiet mode for PHPStan if debug switch is enabled - allows PHPStan debugging
- add allow Composer plugins task

### Changed
- remove useless grouping
- check for PHPUnit configuration file, otherwise skip test run

### Fixed

## [v1.0.0](https://git.d3data.de/D3Public/CI-Actions/release/v1.0.0) - 2025-12-26

### Added
- perform syntax checks before composer to prevent checking non project code
- add log groups for relevant sections
- remove PHPUnit argument because PHPUnit must be a dependency of the current package
- add syntax checks
- add composer package test