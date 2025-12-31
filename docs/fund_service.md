# FundService (class) 🔧

## Purpose
`FundService` is a lightweight, in-memory utility class that encapsulates an array of `Fund` objects and provides simple retrieval and aggregation operations.

## Constructor
```ts
constructor(funds: Fund[])
```
- **Parameter:** `funds` — an array of `Fund` objects used to initialize the service state.
- **Behavior:** The constructor stores the provided array directly (`this.funds = funds`). This means the service does *not* clone the input array; external mutation of the original array will be reflected inside the service.

## Responsibilities
- Provide safe, synchronous accessors such as lookup and filter methods.
- Compute aggregate values for small in-memory datasets.

## Mutability considerations
- Because `FundService` holds a reference to the input array, if callers need isolation they should pass a shallow copy (`[...funds]`) to prevent outside changes from affecting service state.

## Example usage
```ts
const funds: Fund[] = [/* ... */];
const svc = new FundService(funds);
```

## References
- TypeScript classes: https://www.typescriptlang.org/docs/handbook/classes.html
- JSDoc (for documenting class APIs): https://jsdoc.app/
