# FundService.filterByRisk 🔎

## Purpose
Return an array of `Fund` objects whose `riskLevel` matches the provided value.

## Signature
```ts
filterByRisk(level: Fund["riskLevel"]): Fund[]
```

## Parameters
- `level` — One of the string literals: `"Low"`, `"Medium"`, or `"High"`.

## Return value
- An array containing all `Fund` objects with `riskLevel === level`. Returns an empty array if no funds match.

## Example
```ts
const funds = [
  { id: 'F1', name: 'A', riskLevel: 'Low', nav: 100 },
  { id: 'F2', name: 'B', riskLevel: 'High', nav: 200 }
];
const svc = new FundService(funds);
const highRisk = svc.filterByRisk('High');
console.log(highRisk.length); // 1
```

## Edge cases & notes
- The `level` parameter is type-checked by TypeScript; passing arbitrary strings will cause compile-time errors.
- Comparison is strict equality; leading/trailing whitespace or case-differences will not match.

## References
- MDN: Array.prototype.filter — https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter
