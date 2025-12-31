# Fund (Type)

## Purpose

`Fund` is a simple TypeScript data type that models a financial fund's minimal properties used by this module.

## Shape / Responsibilities

- id: string — unique identifier for the fund
- name: string — human-readable fund name
- riskLevel: "Low" | "Medium" | "High" — discrete risk classification used for filtering
- nav: number — net asset value (numeric), used for aggregations

Type definition (from `input.ts`):

export type Fund = {
  id: string;
  name: string;
  riskLevel: "Low" | "Medium" | "High";
  nav: number;
};

## Expected inputs and constraints

- `id` should be unique within any array passed to `FundService` if callers rely on `getFundById` returning a single item.
- `riskLevel` is a union of three literal strings — callers must use exactly "Low", "Medium" or "High".
- `nav` is a number (can be zero or negative depending on domain); numeric precision follows JavaScript number semantics.

## Example

```ts
const fund: Fund = { id: 'f1', name: 'Growth Fund', riskLevel: 'High', nav: 123.45 };
```

## Notes and limitations

- The type enforces allowed `riskLevel` values at compile time but does not validate values at runtime.
- Mutating `Fund` objects after they are stored in `FundService` will affect service results because the implementation stores the provided array reference (see `FundService` docs).

## References

- TypeScript handbook — Basic Types: https://www.typescriptlang.org/docs/handbook/basic-types.html
- TypeScript union types: https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#union-types
