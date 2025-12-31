# Project documentation overview

This repository contains a small TypeScript module that defines a `Fund` data type and a `FundService` class which provides simple read and aggregation operations over an array of `Fund` objects.

Documented features

- `Fund` (type)
  - Purpose, shape, allowed values and example usage
- `FundService` (class)
  - Constructor: initialization and behavior
  - `getFundById(id: string): Fund | undefined`
  - `filterByRisk(level: Fund["riskLevel"]): Fund[]`
  - `calculateAverageNav(): number`

Location of source code

- Primary implementation: `input.ts`

What this documentation covers

- Purpose and responsibilities of each feature
- Public API signatures and return values
- Example usage (TypeScript)
- Edge cases and constraints
- Reference links to TypeScript and relevant MDN documentation
