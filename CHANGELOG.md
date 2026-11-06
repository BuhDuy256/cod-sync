# Changelog

All notable changes to this project are recorded here. Format based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [Unreleased]

### Added

- Phase 0 (domain discovery) in the build workflow, run once before any use case build.
- Domain discovery checklist at `docs/research/domain/README.md`: questions in eight areas, the spec item each area unlocks, and sources to start from.
- Document rule 5 in `WORKFLOW.md`: state content, not provenance.
- Research style rule 11: every source has its exact URL and the date it was read.
- One note file per domain area in `docs/research/domain/`, each linked to its issue.

### Changed

- Product vision: "complaint" replaces "claim", "discrepancy type" replaces "anomaly type" and "error type", and P-5 cites an NFR marker instead of a BR marker.
- Spec templates use ISO dates (`YYYY-MM-DD`).
- Domain questions move from the checklist into one `phase:domain` issue per area (#2–#9), as task lists. The checklist keeps the areas, what each unlocks, and sources.

### Fixed

- Spec gates, templates, and style examples no longer carry content from a previous project; examples now use the COD domain.
- The use case gate no longer lists removed IDs that never existed in this project.
- The vision gate points to `docs/decisions/` instead of `docs/adr/`.
- The research-ticket template's example links point to this repository.
