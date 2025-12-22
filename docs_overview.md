# System Overview

This TypeScript module provides data structures and services for managing financial funds. It includes a `Fund` type that represents individual fund entities and a `FundService` class that offers methods for querying and analyzing fund data.

## Documented Features

- **Fund Type**: Defines the structure of a fund object, including its identifier, name, risk level, and net asset value.
- **FundService Class**: A service class for managing collections of funds, providing methods to retrieve, filter, and calculate statistics on fund data.
  - `getFundById`: Retrieves a specific fund by its ID.
  - `filterByRisk`: Filters funds based on their risk level.
  - `calculateAverageNav`: Computes the average net asset value across all funds.