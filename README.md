
# JSONSQL

**JSONSQL** is a structured, JSON-based query specification designed to express SQL-like queries **safely and consistently**, without exposing raw SQL to clients.

It is inspired by traditional SQL and **CodeIgniter 4 Query Builder**, but redesigned as a **server-driven contract** suitable for APIs, internal services, and delegated development.

---

## Why JSONSQL?

Traditional APIs often struggle with one of these problems:

- Too rigid (many endpoints for small query differences)
- Too dangerous (raw SQL exposure)
- Hard to validate and document
- Difficult to delegate to other developers or partners

JSONSQL solves this by providing:

- ✅ SQL-like expressiveness
- ✅ Strict validation & whitelisting
- ✅ Model-driven schema
- ✅ Predictable mapping to backend query builders
- ✅ Self-documenting structure

---

## What JSONSQL Is (and Is Not)

### JSONSQL **IS**
- A **query contract**
- Structured and machine-validated
- Server-controlled
- Backend-framework friendly
- Suitable for internal & partner APIs

### JSONSQL **IS NOT**
- A raw SQL executor
- A database console
- A replacement for SQL
- A free-form query language

---

## Design Philosophy

> **Clients describe *what* data they want.**  
> **Servers decide *how* the data is retrieved.**

JSONSQL intentionally separates **intent** from **execution**.

---

## Core Features

- SQL-like structure using JSON
- Recursive AND / OR filtering
- Safe operator mapping
- Aggregation and grouping
- Relation inclusion with depth control
- Easy mapping to CodeIgniter 4 Query Builder
- Auto-documentation via model schema

---

## Example Query

```json
{
  "from": "orders",
  "select": ["id", "status", "created_at"],
  "where": {
    "and": [
      { "field": "status", "op": "=", "value": "PAID" },
      { "field": "created_at", "op": "between", "value": ["2026-01-01", "2026-01-31"] }
    ]
  },
  "order_by": [
    { "field": "created_at", "dir": "desc" }
  ],
  "limit": 20
}
````

---

## Typical Use Cases

* Internal admin dashboards
* Partner-facing APIs
* Reporting endpoints
* Delegated backend development
* Query-driven frontend applications

---

## Specification

The complete and authoritative specification is available in:

📄 **[SPEC.md](./SPEC.md)**

This document should be treated as the **contract** for any JSONSQL implementation.

---

## Versioning

* Current version: **JSONSQL v1**
* Backward compatibility is expected within the same major version.

---

## Status

* Specification: **Stable**
* Reference implementation: **Out of scope (by design)**

---

## License

This specification is intended to be open and implementation-agnostic.
See : 📄 **[LICENSE.md](./LICENSE.md)**


---
## Library

At the moment, there is **no official JSONSQL parser or execution library** provided in this repository.

This repository is intentionally maintained as a **SPECIFICATION / CONTRACT ONLY**, serving as a stable and implementation-agnostic reference for anyone who wants to adopt JSONSQL.

However, if you are building or planning to build a **JSONSQL-compatible library** (client-side or server-side), you are very welcome to:

- Implement a JSONSQL parser
- Build a query validator or compiler
- Create a server-side execution engine
- Develop client-side query builders or helpers

### Community Libraries

If you have created a library or tool that follows the JSONSQL specification and would like it to be listed here, please open a pull request and include:

- Library name
- Target language / framework
- Repository URL
- Short description

Once reviewed for specification compliance, your library may be added to this section.

> This approach allows JSONSQL to remain a clean and stable contract while encouraging ecosystem growth through community-driven implementations.

---

## Changelog

All notable changes to the JSONSQL specification are documented and versioned.

➡️ **[CHANGELOG.md](./CHANGELOG.md)**

Any change that affects the JSONSQL contract will be recorded there to maintain transparency and backward compatibility.


---

## Contributing

Contributions are welcome, but please note that this repository is maintained as a
**SPECIFICATION / CONTRACT** repository.

Before submitting a pull request, make sure to read the contribution guidelines:

➡️ **[CONTRIBUTING.md](./CONTRIBUTING.md)**

This helps ensure that all changes preserve the stability and integrity of the JSONSQL specification.

--- 


## Author

**Herlangga Sefani Wijaya**  
Software Engineer & System Architect  
GitHub: https://github.com/gaibz

---

## Contributors

<!-- ALL-CONTRIBUTORS-LIST:START -->
<!-- ALL-CONTRIBUTORS-LIST:END -->


---
© 2026 Herlangga Sefani Wijaya  
This specification is provided "as is" without warranty.

