# Fund (type) 🔧

## Description
A `Fund` represents a financial instrument in the system with identifying metadata and numeric Net Asset Value (NAV). It is a TypeScript type alias used across the module.

## Type definition
```ts
export type Fund = {
  id: string;
  name: string;
  riskLevel: "Low" | "Medium" | "High";
  nav: number;
};
```

## Fields
- `id: string` — Unique identifier for the fund (used as lookup key).
- `name: string` — Human-readable fund name.
- `riskLevel: "Low" | "Medium" | "High"` — Discrete risk classification; callers must use one of these three literal values.
- `nav: number` — Numeric Net Asset Value for the fund.

## Example
```ts
const fund: Fund = {
  id: "FND-001",
  name: "Stable Growth Fund",
  riskLevel: "Low",
  nav: 102.45
};
```

## Notes & constraints
- `riskLevel` is a string literal union — passing other strings will fail TypeScript compile-time checks.
- The module assumes `nav` is a finite number (no NaN/Infinity).

## References
- TypeScript — Basic Types: https://www.typescriptlang.org/docs/handbook/2/everyday-types.html
