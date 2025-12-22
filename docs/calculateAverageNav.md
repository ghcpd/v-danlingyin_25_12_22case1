# FundService.calculateAverageNav ➗

## Purpose
Compute the arithmetic mean of the `nav` field across all stored funds. If no funds are present, the method returns `0`.

## Signature
```ts
calculateAverageNav(): number
```

## Return value
- Returns a `number` representing the average NAV across all funds.
- If `this.funds.length === 0`, returns `0` (explicit handling by the implementation).

## Example
```ts
const funds = [
  { id: 'F1', name: 'A', riskLevel: 'Low', nav: 100 },
  { id: 'F2', name: 'B', riskLevel: 'High', nav: 200 }
];
const svc = new FundService(funds);
console.log(svc.calculateAverageNav()); // 150

const emptySvc = new FundService([]);
console.log(emptySvc.calculateAverageNav()); // 0
```

## Edge cases & notes
- The method sums using `Array.prototype.reduce`. If any `nav` is `NaN` or `Infinity`, the result may be non-finite — callers should ensure input validity.
- No rounding is performed; callers who require a fixed precision should round or format the returned value.

## References
- MDN: Array.prototype.reduce — https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce
