# JSONSQL Schema Notes

This document explains the role, scope, and limitations of the JSON Schema
provided for JSONSQL.

---

## Purpose of the JSON Schema

The JSON Schema included in this repository is designed to:

- Validate the **structural correctness** of JSONSQL requests
- Enforce correct data types and shapes
- Ensure operators, clauses, and nesting follow the specification
- Catch malformed requests early (fail fast)

It serves as a **first line of validation**, not as the sole authority.

---

## What the Schema Validates

The JSON Schema validates:

- Required top-level fields (e.g. `from`)
- Allowed top-level keys
- Structure of `select`, `where`, `order_by`, `include`, `aggregate`
- Recursive boolean expressions (`and` / `or`)
- Operator compatibility with value shapes:
  - `between` requires exactly two values
  - `in` / `not_in` require arrays
  - `is_null` / `not_null` forbid `value`

---

## What the Schema Does NOT Validate

The JSON Schema intentionally does **not** validate:

- Whether a resource exists
- Whether a field is selectable, filterable, or sortable
- Whether an operator is allowed for a specific field
- Relation existence or join correctness
- Authorization rules
- Performance constraints

These checks must be handled by the **server-side validator**.

---

## Why This Separation Exists

JSON Schema is intentionally kept **implementation-agnostic**.

Field-level rules depend on:
- Database schema
- Domain models
- Business logic
- Authorization context

Embedding such rules into a static schema would:
- Make the schema brittle
- Break multi-model compatibility
- Limit reuse across implementations

---

## Recommended Validation Pipeline

A compliant JSONSQL implementation should validate requests in this order:

1. **JSON Schema Validation**
   - Structural correctness
   - Operator/value shape validation

2. **Resource Resolution**
   - Resolve `from` via model registry
   - Reject unknown resources

3. **Model-Aware Validation**
   - Whitelist selectable fields
   - Whitelist filterable fields and operators
   - Validate relations and include depth

4. **Authorization Validation**
   - Apply role-based or tenant-based constraints

5. **Query Execution**
   - Map to query builder
   - Enforce limits and performance safeguards

---

## Design Principle

> JSON Schema validates the **shape** of the query.  
> The server validates the **intent** of the query.

Both are required for a secure and maintainable system.

---

## Final Note

The JSON Schema is a supporting tool, not a replacement for
proper server-side validation.

Any implementation that relies solely on JSON Schema for validation
is considered **non-compliant** with the JSONSQL specification.
