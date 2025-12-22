# Fund Management System - Documentation Overview

## System Description

The Fund Management System provides a service-oriented architecture for managing investment funds. It allows users to retrieve, filter, and analyze fund data with support for risk-level categorization and net asset value (NAV) calculations.

## Documented Features

### 1. **Fund Type** (`Fund`)
- **Purpose**: Data structure representing an investment fund
- **Location**: [input.ts](input.ts)
- **Documentation**: [docs/fund-type.md](docs/fund-type.md)

### 2. **FundService Class**
- **Purpose**: Service for managing and querying fund collections
- **Location**: [input.ts](input.ts)
- **Documentation**: [docs/fund-service.md](docs/fund-service.md)

## Key Capabilities

| Feature | Purpose |
|---------|---------|
| Fund Retrieval | Query individual funds by ID |
| Risk Filtering | Filter funds by risk level (Low/Medium/High) |
| NAV Analysis | Calculate average net asset value across fund portfolio |

## Quick Start

```typescript
// Create a fund service with initial funds
const fundService = new FundService([
  {
    id: "FUND001",
    name: "Conservative Growth",
    riskLevel: "Low",
    nav: 1000.50
  }
]);

// Retrieve a fund by ID
const fund = fundService.getFundById("FUND001");

// Filter funds by risk level
const lowRiskFunds = fundService.filterByRisk("Low");

// Calculate portfolio average NAV
const avgNav = fundService.calculateAverageNav();
```

## Documentation Files

- **[docs/fund-type.md](docs/fund-type.md)** - Complete reference for the `Fund` type
- **[docs/fund-service.md](docs/fund-service.md)** - Complete reference for the `FundService` class

---

**Last Updated**: December 22, 2025
