# Type: Fund

## Purpose
The `Fund` type describes the minimal shape of a financial fund object consumed by `FundService` in this codebase. It is a plain data contract (POJO) with no methods or runtime validation in the current implementation.

## Type definition (from `input.ts`)
- `id: string` — unique identifier for the fund
- `name: string` — human-readable fund name
- `riskLevel: "Low" | "Medium" | "High"` — discrete risk classification used for filtering
- `nav: number` — Net Asset Value (numeric). The code treats this as a raw number (no currency/unit enforced)

## Expected inputs and constraints
- `id` should be unique within a collection managed by `FundService`.
- `nav` is expected to be a finite number. The implementation does not validate positivity or currency; negative or zero NAVs are allowed by the type but should be validated by callers if invalid for your domain.
- `riskLevel` is a string union and will only accept the three literal values shown.

## Usage example
```ts
const f: Fund = { id: 'F-001', name: 'Global Equity', riskLevel: 'High', nav: 12.345 };
```

## Notes & limitations
- No runtime validation: the codebase assumes callers provide well-formed `Fund` objects.
- Units (currency) for `nav` are not specified — document and enforce (e.g., all NAVs in USD) at the application boundary if required.

## References
- TypeScript handbook — Basic Types: https://www.typescriptlang.org/docs/handbook/basic-types.html
- Investopedia — Net Asset Value (NAV): https://www.investopedia.com/terms/n/netassetvalue.asp
