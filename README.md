
## JSON Structure

```json
{
  "name": "Databases",
  "count": 2,
  "items": [
    {
      "name": "Mongodb N. Virginia",
      "statusClass": "ok",
      "type": "Mongodb · AWS / N. Virginia (us-east-1)",
      "metric": "10 ms"
    },
    {
      "name": "Mongodb Lahore",
      "statusClass": "ok",
      "type": "Mongodb · Lahore / JSN WS (LR-1)",
      "metric": "15 ms"
    }
  ]
}
```

## Properties

### `name`

The name of the monitoring category.

**Example:**

```text
Databases
```

---

### `count`

The total number of database services being monitored.

**Example:**

```json
"count": 2
```

The value should match the number of objects inside the `items` array.

---

## `items`

An array containing information about each monitored database service.

Each database contains the following properties:

### `name`

The display name of the database service.

**Example:**

```json
"name": "Mongodb N. Virginia"
```

---

### `statusClass`

Defines the current health status of the database.

Only the following values should be used:

| Value  | Meaning               |
| ------ | --------------------- |
| `ok`   | Operational / Healthy |
| `warn` | Warning / Degraded    |
| `crit` | Critical / Down       |

**Example:**

```json
"statusClass": "ok"
```

The `statusClass` property is the **single source of truth for the database status**. A separate `status` property is not required.

---

### `type`

Describes the database technology and its hosting location or infrastructure.

**Example:**

```json
"type": "Mongodb · AWS / N. Virginia (us-east-1)"
```

Another example:

```json
"type": "Mongodb · Lahore / JSN WS (LR-1)"
```

---

### `metric`

Contains the database response time or another relevant performance metric.

**Example:**

```json
"metric": "10 ms"
```

The value should normally represent the measured response/latency of the database.

## Status Examples

### Operational

```json
{
  "name": "Mongodb N. Virginia",
  "statusClass": "ok",
  "type": "Mongodb · AWS / N. Virginia (us-east-1)",
  "metric": "10 ms"
}
```

### Warning

Use `warn` when the database is available but experiencing degraded performance.

```json
{
  "name": "Mongodb N. Virginia",
  "statusClass": "warn",
  "type": "Mongodb · AWS / N. Virginia (us-east-1)",
  "metric": "150 ms"
}
```

### Critical

Use `crit` when the database is unavailable or experiencing a critical failure.

```json
{
  "name": "Mongodb N. Virginia",
  "statusClass": "crit",
  "type": "Mongodb · AWS / N. Virginia (us-east-1)",
  "metric": "Timeout"
}
```

## Recommended Rules

1. `name` should uniquely identify the database service.
2. `count` should equal the number of objects in `items`.
3. `statusClass` must be one of `ok`, `warn`, or `crit`.
4. Do not add a separate `status` field.
5. `type` should identify the database technology and infrastructure/location.
6. `metric` should contain the latest measured performance value.
7. The frontend should determine the displayed status text from `statusClass`.

### Status Mapping

```javascript
const statusMap = {
  ok: "Operational",
  warn: "Warning",
  crit: "Critical"
};
```

This keeps the JSON structure simple while allowing the frontend to control the visual representation and status text.


**Reporting Bugs**
If you find an issue with EasyCSS, please report it via the GitHub issue tracker and via E-mail : github@jalsonic.com. 

Designed, Built and Maintained by [Jalsonic Networks Teams](https://www.jalsonic.com) 2025. 
A Division of [Jalsonic Networks](https://www.jalsonic.com) 2025.
