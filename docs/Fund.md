# Fund Type

## Feature Description

The `Fund` type represents a financial fund entity in the system. It encapsulates the essential properties of a fund, including its unique identifier, name, risk level, and net asset value (NAV). This type is used throughout the application to ensure type safety when working with fund data.

## API Reference

```typescript
export type Fund = {
  id: string;
  name: string;
  riskLevel: "Low" | "Medium" | "High";
  nav: number;
};
```

### Fields

- `id: string` - A unique identifier for the fund.
- `name: string` - The human-readable name of the fund.
- `riskLevel: "Low" | "Medium" | "High"` - The risk classification of the fund, limited to predefined levels.
- `nav: number` - The net asset value of the fund, representing the value per share.

## Example Usage

```typescript
import { Fund } from './input';

const sampleFund: Fund = {
  id: 'fund-001',
  name: 'Global Equity Fund',
  riskLevel: 'Medium',
  nav: 150.75
};
```

## Notes and Limitations

- The `riskLevel` is restricted to the three predefined string literals to maintain consistency.
- The `nav` field should be a positive number; negative values may indicate data errors.

## References

- [TypeScript Handbook - Object Types](https://www.typescriptlang.org/docs/handbook/2/objects.html)
- [Investopedia - Net Asset Value (NAV)](https://www.investopedia.com/terms/n/nav.asp)