# Class: FundService

Provides simple in-memory queries and aggregations over an array of `Fund` objects.

Files: `input.ts`

## Purpose & responsibilities
- Hold an in-memory collection of `Fund` objects provided at construction time.
- Provide read/query operations: lookup by id, filter by risk level, and compute average NAV.
- This class does not persist data or perform validation beyond in-memory operations.

## Constructor
### Signature
```ts
constructor(funds: Fund[])
```

### Behavior
- Stores a reference to the provided `funds` array as-is (no deep clone). Mutating the original array after constructing `FundService` will affect the service's internal state.
- There is no runtime validation: passing `null`, `undefined`, or a non-array will lead to runtime errors when methods run.

### Example
```ts
const funds = [{ id: 'a', name: 'A', riskLevel: 'Low', nav: 10 }];
const svc = new FundService(funds);
funds.push({ id: 'b', name: 'B', riskLevel: 'High', nav: 5 }); // svc sees this change
```

### Notes / Recommendation
- If callers should not be able to mutate internal state, change the constructor to clone the array (e.g. `this.funds = funds.slice()` or deep-clone) and add runtime validation.

## getFundById
### Signature
```ts
getFundById(id: string): Fund | undefined
```

### Purpose
Return the first `Fund` whose `id` matches the provided `id` string.

### Inputs
- `id` — string identifier to match against `Fund.id`.

### Returns
- `Fund` when a match is found.
- `undefined` when no fund with the given `id` exists.

### Complexity
- Time: O(n) — uses linear search via `Array.prototype.find`.

### Edge cases
- `id` not present → returns `undefined` (caller must handle this).
- Duplicate `id`s in the array → returns the first match.
- Non-string `id` (at runtime) may not match; the method expects a `string`.

### Example
```ts
svc.getFundById('a'); // -> { id: 'a', ... }
svc.getFundById('missing'); // -> undefined
```

### References
- MDN: Array.prototype.find — https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array/find

## filterByRisk

### Signature
```ts
filterByRisk(level: Fund["riskLevel"]): Fund[]
```

### Purpose
Return all funds whose `riskLevel` strictly equals the provided `level`.

### Inputs
- `level` — one of the string literals: `"Low" | "Medium" | "High"`.

### Returns
- A new array (may be empty) containing matching `Fund` objects.

### Complexity
- Time: O(n)
- Returns a shallow copy of matched elements (does not deep-clone each fund).

### Edge cases
- If no funds match, returns `[]` (empty array).
- Passing an invalid string at runtime will simply return `[]` (no matches) — the TypeScript type prevents this at compile time.

### Example
```ts
svc.filterByRisk('Low'); // -> [{ id: 'a', ... }]
svc.filterByRisk('Medium'); // -> []
```

### References
- MDN: Array.prototype.filter — https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array/filter

## calculateAverageNav

### Signature
```ts
calculateAverageNav(): number
```

### Purpose
Compute the arithmetic mean of the `nav` values of all funds currently held by the service.

### Returns
- The numeric average of all `nav` values.
- Returns `0` when there are no funds (explicit in implementation).

### Formula
If there are N funds with NAVs \(v_1, \dots, v_N\), the method returns

$$\text{average} = \frac{1}{N}\sum_{i=1}^{N} v_i$$

If N = 0, the method returns 0.

### Complexity
- Time: O(n)
- Space: O(1)

### Edge cases & numeric notes
- Empty list → `0` (documented here; callers relying on `NaN` should adjust).
- Negative NAV values are included in the average because there is no validation (caller responsibility).
- No rounding is performed; floating-point results may include usual IEEE-754 artifacts. Consider `Number.toFixed` or a decimal library for presentation/financial accuracy.
- Very large arrays or very large NAV values can introduce floating-point precision loss; use aggregation strategies or BigInt/decimal libraries for high-precision financial calculations.

### Example
```ts
const svc = new FundService([
  { id: 'a', name: 'A', riskLevel: 'Low', nav: 10 },
  { id: 'b', name: 'B', riskLevel: 'High', nav: 20 }
]);
svc.calculateAverageNav(); // -> 15

const empty = new FundService([]);
empty.calculateAverageNav(); // -> 0
```

### References
- MDN: Array.prototype.reduce — https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce
- IEEE-754 and floating point caveats — https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number#floating-point_arithmetic

## Suggested quick JSDoc additions (copy/paste)
Add the following to `input.ts` above each symbol to provide inline docs and improve IDE/TS inference:

```ts
/**
 * Minimal representation of a financial fund used by the application.
 */
export type Fund = { ... }

/**
 * Manage an in-memory collection of funds and provide basic queries.
 * @param funds - array of Fund objects (the array is stored by reference)
 */
constructor(funds: Fund[]) { ... }
```

