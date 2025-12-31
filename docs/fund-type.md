# Fund Type Reference

## Overview

The `Fund` type is the core data model in the fund management system. It represents an investment fund with essential attributes for portfolio management and analysis.

## Type Definition

```typescript
export type Fund = {
  id: string;
  name: string;
  riskLevel: "Low" | "Medium" | "High";
  nav: number;
};
```

## Properties

### `id` (string)
- **Description**: Unique identifier for the fund
- **Purpose**: Used to distinguish funds and support lookups by ID
- **Requirements**: Must be unique within a fund collection
- **Example**: `"FUND001"`, `"EQUITY-GROWTH-2024"`

### `name` (string)
- **Description**: Human-readable name of the fund
- **Purpose**: Display name for fund identification in user interfaces and reports
- **Example**: `"Conservative Growth Fund"`, `"Tech Innovation Fund"`

### `riskLevel` ("Low" | "Medium" | "High")
- **Description**: Risk classification of the fund
- **Purpose**: Categorizes funds by investment risk profile for filtering and analysis
- **Valid Values**:
  - `"Low"` - Conservative investments with lower volatility
  - `"Medium"` - Balanced risk-return profile
  - `"High"` - Aggressive investments with higher volatility
- **Example**: `"Medium"`

### `nav` (number)
- **Description**: Net Asset Value - the per-unit value of the fund
- **Purpose**: Used for valuation calculations and portfolio analysis
- **Format**: Decimal number representing currency amount
- **Constraints**: Should be a positive number
- **Example**: `1000.50`, `2543.75`

## Usage Examples

### Creating a Fund Object

```typescript
const aggressiveGrowthFund: Fund = {
  id: "AGG-GROWTH-01",
  name: "Aggressive Growth Portfolio",
  riskLevel: "High",
  nav: 1500.75
};
```

### Array of Funds (Common Pattern)

```typescript
const fundPortfolio: Fund[] = [
  {
    id: "LOW-001",
    name: "Fixed Income Fund",
    riskLevel: "Low",
    nav: 950.25
  },
  {
    id: "MED-001",
    name: "Balanced Fund",
    riskLevel: "Medium",
    nav: 1200.50
  },
  {
    id: "HIGH-001",
    name: "Equity Fund",
    riskLevel: "High",
    nav: 1650.00
  }
];
```

## Constraints & Considerations

- **Uniqueness**: The `id` property should be unique across all funds in a collection
- **NAV Values**: Typically positive numbers; negative NAV values may indicate edge cases
- **Risk Level**: Only three predefined levels are supported; custom risk categories are not supported
- **Immutability**: Consider treating individual `Fund` objects as immutable after creation

## Related Components

- **FundService**: Service class for querying and analyzing `Fund` objects
- See [docs/fund-service.md](fund-service.md) for service methods that operate on funds

## References

- **TypeScript Type Aliases**: https://www.typescriptlang.org/docs/handbook/2/types-from-types.html#type-aliases
- **Union Types in TypeScript**: https://www.typescriptlang.org/docs/handbook/2/narrowing.html

---

**Last Updated**: December 22, 2025
