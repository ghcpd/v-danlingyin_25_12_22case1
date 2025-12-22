# FundService.getFundById 🎯

## Purpose
Return a single `Fund` whose `id` matches the provided value, or `undefined` when not found.

## Signature
```ts
getFundById(id: string): Fund | undefined
```

## Parameters
- `id` (`string`) — The fund identifier to search for.

## Return value
- Returns the first matching `Fund` object, or `undefined` if no fund has the provided `id`.

## Example
```ts
const funds: Fund[] = [
  { id: 'F1', name: 'Alpha', riskLevel: 'Medium', nav: 120 },
  { id: 'F2', name: 'Beta', riskLevel: 'Low', nav: 95 }
];
const service = new FundService(funds);

const fund = service.getFundById('F1');
if (fund) {
  console.log(fund.name); // 'Alpha'
} else {
  // handle not-found
}
```

## Edge cases & notes
- If multiple funds share an `id` (which should be avoided), this method returns the first match.
- The function uses a simple linear search (`Array.prototype.find`) so it is O(N) in the number of funds.
- Callers must handle the `undefined` result to avoid runtime errors.

## References
- MDN: Array.prototype.find — https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find
