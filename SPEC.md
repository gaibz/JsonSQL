
# JSONSQL v1 Specification

**Version:** 1.0  
**Status:** Stable  
**Type:** Query Contract

---

## 1. Overview

JSONSQL is a structured JSON-based query specification designed to safely represent SQL-like queries in API environments.

It prioritizes:
- Security
- Predictability
- Validation
- Long-term maintainability

---

## 2. Top-Level Structure

```json
{
  "from": "resource",
  "select": [],
  "where": {},
  "order_by": [],
  "limit": 0,
  "offset": 0,
  "include": {},
  "group_by": [],
  "having": {},
  "aggregate": []
}
````

---

## 3. `from` (Required)

```json
"from": "orders"
```

### Rules

* Required
* String
* Must match a registered resource
* Must NOT reference raw table names

---

## 4. `select`

### Simple

```json
"select": ["id", "status"]
```

### With Alias

```json
"select": [
  "id",
  { "field": "created_at", "as": "createdAt" }
]
```

### Rules

* Fields must be explicitly allowed by the server
* No SQL functions or expressions allowed

---

## 5. `where`

The `where` clause is a **recursive boolean expression**.

### Expression (Leaf Node)

```json
{
  "field": "status",
  "op": "=",
  "value": "PAID"
}
```

### AND Group

```json
{
  "and": [
    { "field": "status", "op": "=", "value": "PAID" },
    { "field": "total", "op": ">", "value": 100000 }
  ]
}
```

### OR Group

```json
{
  "or": [
    { "field": "status", "op": "=", "value": "PAID" },
    { "field": "status", "op": "=", "value": "SHIPPED" }
  ]
}
```

### Nested Groups

```json
{
  "and": [
    { "field": "company_id", "op": "=", "value": 10 },
    {
      "or": [
        { "field": "status", "op": "=", "value": "PAID" },
        { "field": "status", "op": "=", "value": "SHIPPED" }
      ]
    }
  ]
}
```

---

## 6. Operators

| Operator      | Description           |
| ------------- | --------------------- |
| `=`           | Equal                 |
| `!=`          | Not equal             |
| `>`           | Greater than          |
| `>=`          | Greater than or equal |
| `<`           | Less than             |
| `<=`          | Less than or equal    |
| `in`          | In array              |
| `not_in`      | Not in array          |
| `like`        | LIKE                  |
| `not_like`    | NOT LIKE              |
| `starts_with` | LIKE value%           |
| `ends_with`   | LIKE %value           |
| `contains`    | LIKE %value%          |
| `between`     | Range (min, max)      |
| `is_null`     | IS NULL               |
| `not_null`    | IS NOT NULL           |

---

## 7. `order_by`

```json
"order_by": [
  { "field": "created_at", "dir": "desc" }
]
```

### Rules

* Fields must be sortable
* `dir` must be `asc` or `desc`

---

## 8. Pagination

```json
"limit": 50,
"offset": 0
```

### Rules

* Server must enforce maximum limits
* Offset must be non-negative

---

## 9. `include` (Relations)

```json
"include": {
  "customer": {
    "select": ["id", "name"]
  }
}
```

### Rules

* Relations must be explicitly defined server-side
* Arbitrary joins are not allowed
* Depth should be limited

---

## 10. Aggregation

```json
"aggregate": [
  { "fn": "count", "as": "total" },
  { "fn": "sum", "field": "grand_total", "as": "amount" }
]
```

### Supported Functions

* `count`
* `sum`
* `avg`
* `min`
* `max`

---

## 11. `group_by` and `having`

```json
"group_by": ["status"],
"having": {
  "and": [
    { "field": "total", "op": ">", "value": 10 }
  ]
}
```

---

## 12. Validation Rules (Mandatory)

Implementations MUST:

1. Validate resources
2. Whitelist selectable, filterable, and sortable fields
3. Validate operators per field
4. Enforce query limits
5. Reject raw SQL or executable expressions

---

## 13. Security Model

JSONSQL is secure by design because it:

* Uses structured JSON instead of strings
* Avoids SQL parsing entirely
* Enforces server-side intent validation
* Relies on safe query builders

---

## 14. Versioning

```json
{
  "version": "1.0"
}
```

* Versioning is explicit
* Backward compatibility is expected within major versions

---

## 15. Non-Goals

JSONSQL explicitly does NOT support:

* Raw SQL execution
* Arbitrary joins
* Subqueries
* Stored procedures
* Database-specific syntax

---

## 16. Contract Statement

> JSONSQL is a **contract**, not an execution engine.
> Any implementation must respect this specification to be considered compliant.
