# Data & Rule Modeling

## Canonical identity

External data should be mapped to internal identities before calculations depend on it.

For airports, stable identifiers such as ICAO codes are useful, but source-specific aliases may still be required.

```text
external record
      ↓
identifier mapping
      ↓
canonical airport / aircraft
      ↓
validated attributes
```

## Units

Units should be explicit.

Values such as:

```text
75 tonnes
75,000 kg
165,347 lb
```

can describe the same aircraft mass but cannot safely be treated as interchangeable raw numbers.

Normalization should happen at a clear boundary before rule evaluation.

## Generic rule shape

A conceptual rule representation could contain:

```ts
type ChargeRule = {
  type: ChargeType;
  jurisdiction: Jurisdiction;
  basis: ChargeBasis;
  currency: string;
  effectiveFrom?: Date;
  effectiveTo?: Date;
  minimum?: Money;
  conditions: Condition[];
  formula: Formula;
  source?: SourceReference;
};
```

This is illustrative rather than production source code.

## Structured output

The engine should return structured components rather than only a scalar total.

```ts
type ChargeResult = {
  type: ChargeType;
  amount: number;
  currency: string;
  basis?: string;
  quantity?: number;
  rate?: number;
  explanation: string;
};
```

Structured output improves UI presentation, testing, troubleshooting, and auditability.
