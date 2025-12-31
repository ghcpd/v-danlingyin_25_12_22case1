# FundService Class

## Feature Description

The `FundService` class is a service component designed to manage and query collections of `Fund` objects. It provides methods for retrieving individual funds, filtering by risk level, and calculating aggregate statistics. This class acts as the primary interface for fund data operations in the application.

## API Reference

```typescript
export class FundService {
  constructor(funds: Fund[]);
  getFundById(id: string): Fund | undefined;
  filterByRisk(level: Fund["riskLevel"]): Fund[];
  calculateAverageNav(): number;
}
```

### Constructor

- `constructor(funds: Fund[])` - Initializes the service with an array of `Fund` objects.

### Methods

#### getFundById(id: string): Fund | undefined

Retrieves a fund by its unique identifier.

**Parameters:**
- `id: string` - The unique identifier of the fund to retrieve.

**Returns:** `Fund | undefined` - The fund object if found, or `undefined` if no fund matches the ID.

#### filterByRisk(level: Fund["riskLevel"]): Fund[]

Filters the funds based on their risk level.

**Parameters:**
- `level: Fund["riskLevel"]` - The risk level to filter by ("Low", "Medium", or "High").

**Returns:** `Fund[]` - An array of funds matching the specified risk level.

#### calculateAverageNav(): number

Calculates the average net asset value across all funds.

**Parameters:** None

**Returns:** `number` - The average NAV value. Returns 0 if there are no funds.

## Example Usage

```typescript
import { FundService, Fund } from './input';

const funds: Fund[] = [
  { id: '1', name: 'Low Risk Fund', riskLevel: 'Low', nav: 100 },
  { id: '2', name: 'Medium Risk Fund', riskLevel: 'Medium', nav: 150 },
  { id: '3', name: 'High Risk Fund', riskLevel: 'High', nav: 200 }
];

const service = new FundService(funds);

// Get a specific fund
const fund = service.getFundById('2');
console.log(fund?.name); // 'Medium Risk Fund'

// Filter by risk
const lowRiskFunds = service.filterByRisk('Low');
console.log(lowRiskFunds.length); // 1

// Calculate average NAV
const averageNav = service.calculateAverageNav();
console.log(averageNav); // 150
```

## Notes and Limitations

- The service does not modify the original funds array; all operations are read-only.
- If the funds array is empty, `calculateAverageNav` returns 0 to avoid division by zero.
- Methods assume valid input data; no additional validation is performed.

## References

- [TypeScript Handbook - Classes](https://www.typescriptlang.org/docs/handbook/2/classes.html)
- [MDN Web Docs - Array.prototype.find](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)
- [MDN Web Docs - Array.prototype.filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)