# FundService (class)

## Purpose

`FundService` provides small, synchronous read and aggregation operations over an in-memory array of `Fund` objects. It does not perform network I/O or persistence — it is a lightweight utility for accessing and summarizing fund data held in memory.

Source: `input.ts`

## Responsibilities

- Hold a reference to an array of `Fund` objects supplied at construction time.
- Provide methods to find a fund by id, filter funds by risk level, and compute the average NAV.

## Constructor

Signature

```ts
constructor(funds: Fund[])
```

Parameters

- `funds`: an array of `Fund` objects. The constructor assigns the provided array reference to an internal field (`this.funds`). The array is not defensively copied.

Behavior / Constraints

- Mutating the `funds` array after passing it to the constructor will affect the `FundService` instance (shared reference).
- Passing an empty array is allowed; aggregation methods handle empty arrays explicitly.

## Public API

### getFundById(id: string): Fund | undefined

- Purpose: Return the first `Fund` whose `id` strictly equals the supplied `id`.
- Parameters: `id` — string identifier to match.
- Returns: the matching `Fund` or `undefined` if no match is found.
- Notes: Uses array `find`; returns the first match when duplicates exist.

Example

```ts
const svc = new FundService([{ id: 'a', name: 'A', riskLevel: 'Low', nav: 10 }]);
const f = svc.getFundById('a');
// f === { id: 'a', name: 'A', riskLevel: 'Low', nav: 10 }
const none = svc.getFundById('missing');
// none === undefined
```

### filterByRisk(level: Fund["riskLevel"]): Fund[]

- Purpose: Return an array of funds whose `riskLevel` matches the provided value.
- Parameters: `level` — one of `"Low" | "Medium" | "High"`.
- Returns: array of `Fund` objects matching the risk level; returns an empty array when there are no matches.

Example

```ts
const svc = new FundService([
  { id: 'a', name: 'A', riskLevel: 'Low', nav: 10 },
  { id: 'b', name: 'B', riskLevel: 'High', nav: 20 }
]);
const low = svc.filterByRisk('Low');
// low.length === 1
const none = svc.filterByRisk('Medium');
// none.length === 0
```

### calculateAverageNav(): number

- Purpose: Compute the arithmetic mean of the `nav` values of the service's funds.
- Parameters: none
- Returns: numeric average (TypeScript `number`). If the service contains zero funds, the method returns `0`.

Edge cases / behavior

- Empty funds array -> returns `0` (explicit guard in implementation).
- Negative or zero `nav` values are included in the arithmetic calculation.
- Numeric precision follows JavaScript `number` rules (IEEE-754 double precision).

Example

```ts
const svc = new FundService([
  { id: 'a', name: 'A', riskLevel: 'Low', nav: 10 },
  { id: 'b', name: 'B', riskLevel: 'High', nav: 20 }
]);
const avg = svc.calculateAverageNav();
// avg === 15

const emptySvc = new FundService([]);
emptySvc.calculateAverageNav(); // 0
```

## Implementation notes

- The class stores the provided `funds` array reference directly (no copy), so callers should pass either an immutable array or be aware that later modifications will be observed by `FundService`.
- Methods are synchronous and side-effect free (they do not mutate `this.funds`).

## References

- TypeScript classes: https://www.typescriptlang.org/docs/handbook/classes.html
- Array.prototype.find — MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find
- Array.prototype.filter — MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter
- Array.prototype.reduce — MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce
