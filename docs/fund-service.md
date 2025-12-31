# FundService Class Reference

## Overview

The `FundService` class provides a service layer for managing and querying a collection of investment funds. It offers methods for fund retrieval, filtering by risk level, and portfolio analysis through NAV calculations.

## Class Definition

```typescript
export class FundService {
  private funds: Fund[];
  
  constructor(funds: Fund[])
  getFundById(id: string): Fund | undefined
  filterByRisk(level: Fund["riskLevel"]): Fund[]
  calculateAverageNav(): number
}
```

## Constructor

### `constructor(funds: Fund[])`

**Purpose**: Initialize the FundService with an array of funds

**Parameters**:
- `funds` (Fund[]): Initial array of fund objects to manage

**Behavior**:
- Stores the funds array for use by all service methods
- Creates a reference to the provided array (not a deep copy)

**Example**:

```typescript
const fundList: Fund[] = [
  { id: "FUND001", name: "Growth Fund", riskLevel: "High", nav: 1500 },
  { id: "FUND002", name: "Safe Fund", riskLevel: "Low", nav: 900 }
];

const fundService = new FundService(fundList);
```

## Methods

### `getFundById(id: string): Fund | undefined`

**Purpose**: Retrieve a single fund by its unique identifier

**Parameters**:
- `id` (string): The unique identifier of the fund to retrieve

**Returns**:
- `Fund` object if found
- `undefined` if no fund matches the given ID

**Throws**: None (returns undefined for not found)

**Example**:

```typescript
const fund = fundService.getFundById("FUND001");

if (fund) {
  console.log(`Found: ${fund.name} with NAV ${fund.nav}`);
} else {
  console.log("Fund not found");
}
```

**Performance**: O(n) - Linear search through the funds array

**Edge Cases**:
- Returns `undefined` if funds array is empty
- Returns `undefined` if no matching ID is found
- Case-sensitive ID matching

---

### `filterByRisk(level: Fund["riskLevel"]): Fund[]`

**Purpose**: Retrieve all funds matching a specific risk level

**Parameters**:
- `level` (Fund["riskLevel"]): Risk level to filter by
  - Valid values: `"Low"`, `"Medium"`, `"High"`

**Returns**:
- Array of `Fund` objects matching the specified risk level
- Empty array if no funds match or funds array is empty

**Throws**: None

**Example**:

```typescript
// Get all low-risk funds
const conservativeFunds = fundService.filterByRisk("Low");
console.log(`Found ${conservativeFunds.length} low-risk funds`);

conservativeFunds.forEach(fund => {
  console.log(`- ${fund.name}: NAV ${fund.nav}`);
});
```

**Performance**: O(n) - Scans entire funds array

**Edge Cases**:
- Returns empty array if no funds match the risk level
- Returns empty array if funds array is empty
- Risk level matching is case-sensitive (must be exact case)

---

### `calculateAverageNav(): number`

**Purpose**: Calculate the average Net Asset Value (NAV) across all funds in the portfolio

**Parameters**: None

**Returns**:
- `number`: The average NAV across all funds
- `0` if the funds array is empty (no division by zero)

**Throws**: None

**Formula**: $\text{Average NAV} = \frac{\sum_{i=0}^{n-1} \text{fund}_i.\text{nav}}{n}$

**Example**:

```typescript
const avgNav = fundService.calculateAverageNav();
console.log(`Portfolio average NAV: $${avgNav.toFixed(2)}`);

// Example with actual values:
// Funds: [1000, 1500, 900]
// Average: (1000 + 1500 + 900) / 3 = 1133.33
```

**Performance**: O(n) - Iterates through all funds once

**Edge Cases**:
- Returns `0` if funds array is empty (prevents division by zero)
- Includes all funds regardless of risk level
- Result may be a decimal number; consider rounding for display

---

## Complete Usage Example

```typescript
// Initialize with sample data
const funds: Fund[] = [
  {
    id: "BALANCED-001",
    name: "Balanced Portfolio",
    riskLevel: "Medium",
    nav: 1200.00
  },
  {
    id: "CONSERVATIVE-001",
    name: "Conservative Bond Fund",
    riskLevel: "Low",
    nav: 950.50
  },
  {
    id: "AGGRESSIVE-001",
    name: "Tech Growth Fund",
    riskLevel: "High",
    nav: 1800.75
  },
  {
    id: "CONSERVATIVE-002",
    name: "Money Market Fund",
    riskLevel: "Low",
    nav: 1000.00
  }
];

const fundService = new FundService(funds);

// Use Case 1: Find a specific fund
const targetFund = fundService.getFundById("BALANCED-001");
if (targetFund) {
  console.log(`Found fund: ${targetFund.name}`);
}

// Use Case 2: Filter by risk level
const conservativeFunds = fundService.filterByRisk("Low");
console.log(`Conservative funds count: ${conservativeFunds.length}`);
// Output: Conservative funds count: 2

// Use Case 3: Calculate portfolio metrics
const avgNav = fundService.calculateAverageNav();
console.log(`Average portfolio NAV: $${avgNav.toFixed(2)}`);
// Output: Average portfolio NAV: $1238.06
```

## Design Considerations

### Immutability
- The service stores a reference to the funds array, not a copy
- External modifications to the source array will affect service results
- Consider creating a defensive copy if immutability is required

### Thread Safety
- This class is not thread-safe
- Concurrent access should be managed at a higher level

### Performance Characteristics

| Method | Time Complexity | Space Complexity |
|--------|-----------------|------------------|
| Constructor | O(1) | O(1) |
| getFundById | O(n) | O(1) |
| filterByRisk | O(n) | O(k) - where k is result size |
| calculateAverageNav | O(n) | O(1) |

### Future Enhancements
- Add indexing by ID for O(1) lookups
- Support more granular filtering options
- Add fund update/delete operations

## References

- **TypeScript Classes**: https://www.typescriptlang.org/docs/handbook/2/classes.html
- **Array Methods (find, filter, reduce)**: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array
- **Defensive Copying**: https://en.wikipedia.org/wiki/Defensive_copy

---

**Last Updated**: December 22, 2025
