# System overview ✅

## What this module does

This small module models simple fund data and provides an in-memory service for basic lookups and aggregations.

- **Data model:** `Fund` — a typed representation of a fund, with id, name, risk level and NAV.
- **Service:** `FundService` — an in-memory service that stores an array of `Fund` objects and exposes methods to query and compute aggregate values.

## Documented features

- `Fund` (type) — definition and field descriptions
- `FundService` (class) — purpose and constructor notes
- `FundService#getFundById` — API reference, return semantics
- `FundService#filterByRisk` — API reference, usage
- `FundService#calculateAverageNav` — API reference, behaviour on empty state

---

> Note: Detailed docs are available per-feature in the `docs/` directory (one file per feature).

References
- TypeScript handbook (types & classes): https://www.typescriptlang.org/docs/handbook/2/everyday-types.html
- JSDoc reference for documenting APIs: https://jsdoc.app/
- MDN: Array.prototype.find / filter / reduce: https://developer.mozilla.org/en-US/
