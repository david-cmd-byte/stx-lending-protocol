# STX Lending Protocol

A secure, decentralized lending protocol built on the Stacks blockchain that enables users to deposit STX tokens as collateral, borrow against their positions, and participate in liquidations.

## Overview

The STX Lending Protocol is a decentralized finance (DeFi) solution that implements a secure lending and borrowing system on the Stacks blockchain. It enables users to participate in collateralized lending operations while maintaining protocol solvency through carefully designed safety mechanisms.

### Key Features

- **Collateralized Borrowing**: Users can deposit STX tokens as collateral and borrow against their positions
- **Dynamic Interest Rates**: Interest calculations based on time and amount borrowed
- **Liquidation Mechanism**: Automatic liquidation of under-collateralized positions to maintain protocol solvency
- **Flexible Parameters**: Adjustable protocol parameters managed by contract owner
- **Safety First**: Multiple safety checks and minimum collateral requirements

## Protocol Parameters

| Parameter                | Default Value | Description                                              |
| ------------------------ | ------------- | -------------------------------------------------------- |
| Minimum Collateral Ratio | 150%          | Minimum required collateral-to-debt ratio                |
| Liquidation Threshold    | 130%          | Ratio at which positions become eligible for liquidation |
| Protocol Fee             | 1%            | Fee charged on borrowing operations                      |
| Maximum Collateral Ratio | 500%          | Upper limit for collateral ratio                         |
| Minimum Required Ratio   | 110%          | Absolute minimum collateral ratio allowed                |

## Core Functions

### For Users

#### Deposit

```clarity
(define-public (deposit))
```

Allows users to deposit STX tokens as collateral. The amount is automatically calculated based on the sender's balance.

#### Borrow

```clarity
(define-public (borrow (amount uint)))
```

Enables users to borrow STX against their deposited collateral, maintaining the minimum collateral ratio.

#### Repay

```clarity
(define-public (repay (amount uint)))
```

Allows users to repay their borrowed amounts, reducing their debt position.

#### Withdraw

```clarity
(define-public (withdraw (amount uint)))
```

Enables users to withdraw their collateral if the remaining position maintains the minimum collateral ratio.

### For Liquidators

#### Liquidate

```clarity
(define-public (liquidate (user principal)))
```

Allows liquidators to liquidate positions that fall below the liquidation threshold, helping maintain protocol solvency.

### For Administrators

#### Set Minimum Collateral Ratio

```clarity
(define-public (set-minimum-collateral-ratio (new-ratio uint)))
```

Allows the contract owner to adjust the minimum required collateral ratio (between 110% and 500%).

#### Set Liquidation Threshold

```clarity
(define-public (set-liquidation-threshold (new-threshold uint)))
```

Enables adjustment of the liquidation threshold, which must be below the minimum collateral ratio.

#### Set Protocol Fee

```clarity
(define-public (set-protocol-fee (new-fee uint)))
```

Allows modification of the protocol fee (maximum 10%).

## Read-Only Functions

### Get User Position

```clarity
(define-read-only (get-user-position (user principal)))
```

Returns the current position of a user, including:

- Total collateral deposited
- Total amount borrowed
- Number of active loans

### Get Protocol Stats

```clarity
(define-read-only (get-protocol-stats))
```

Returns current protocol statistics:

- Total deposits
- Total borrows
- Current minimum collateral ratio
- Current liquidation threshold
- Current protocol fee

## Error Codes

| Code                               | Description                               |
| ---------------------------------- | ----------------------------------------- |
| ERR-NOT-AUTHORIZED (u100)          | Caller not authorized for this operation  |
| ERR-INSUFFICIENT-COLLATERAL (u101) | Collateral ratio would fall below minimum |
| ERR-INVALID-AMOUNT (u102)          | Invalid amount specified for operation    |
| ERR-LOAN-NOT-FOUND (u103)          | Referenced loan does not exist            |
| ERR-LOAN-ACTIVE (u104)             | Loan is still active                      |
| ERR-INSUFFICIENT-BALANCE (u105)    | Insufficient balance for operation        |
| ERR-LIQUIDATION-FAILED (u106)      | Liquidation conditions not met            |
| ERR-INVALID-PARAMETER (u107)       | Invalid parameter value provided          |

## Security Considerations

1. **Collateral Safety**: Multiple checks ensure collateral ratios remain healthy
2. **Liquidation Protection**: Self-liquidation is prevented
3. **Parameter Bounds**: All adjustable parameters have strict bounds
4. **Access Control**: Administrative functions restricted to contract owner
5. **Safe Math**: Built-in Clarity arithmetic prevents overflows

## Development

### Prerequisites

- Clarity CLI
- Stacks blockchain local development environment
- Node.js and npm (for testing environment)

### Testing

Comprehensive test coverage includes:

- Deposit/withdraw functionality
- Borrowing mechanisms
- Liquidation scenarios
- Administrative controls
- Edge cases and error conditions

## Contributing

Contributions are welcome! Please read our contributing guidelines before submitting pull requests.
