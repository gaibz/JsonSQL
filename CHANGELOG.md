# Changelog

All notable changes to this project will be documented in this file.

This project follows a structured change management process to ensure the
stability and backward compatibility of the JSONSQL specification.

---

## [Unreleased]

### Added
- Initial public draft of the JSONSQL specification.

### Changed
- N/A

### Deprecated
- N/A

### Removed
- N/A

### Fixed
- N/A

---

## [1.0.0] - 2026-01-08

### Added
- JSONSQL v1 specification.
- Structured JSON-based query contract inspired by SQL and CodeIgniter 4 Query Builder.
- Support for:
  - Resource-based querying (`from`)
  - Field selection with aliasing
  - Recursive `where` clauses (AND / OR)
  - Sorting via `order_by`
  - Pagination (`limit`, `offset`)
  - Aggregation functions
  - Grouping and `having` clauses
  - Relation inclusion (`include`)
- Security and validation rules.
- Clear separation between query intent and execution.

### Changed
- N/A

### Deprecated
- N/A

### Removed
- N/A

### Fixed
- N/A

---

## Versioning Policy

- **Major versions** introduce breaking changes.
- **Minor versions** add backward-compatible features or clarifications.
- **Patch versions** include documentation fixes or non-functional changes.

---

## Notes

This changelog is maintained manually to preserve clarity and intent.

Any change that affects the JSONSQL contract must be documented here.
