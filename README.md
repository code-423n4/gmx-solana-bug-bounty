# GMX-Solana Bug Bounty

- [Read our guidelines for more details](https://docs.code4rena.com/bounties)
- Submit findings [using the C4 form](https://code4rena.com/bounties/gmx-solana/submit)

| Risk Score |  Payout |
|------------|---------|
| Critical   | The reward cap would be the mininum of - 10% of funds at risk - $200,000 USDC - 10\% of the treasury <br> With a proposed minimum reward of $25,000, not exceeding the cap. |
| High       | $10,000 USDC - $25,000 USDC |
| Medium | $5,000 USDC - $10,000 USDC |

## Background on GMX-Solana

### What is GMX-Solana

GMX-Solana is a decentralized leveraged trading platform built on the Solana blockchain, drawing inspiration from the technical innovations introduced by [GMX V2](https://docs.gmx.io/docs/intro). The platform aims to provide a seamless trading experience with fast transaction times and low fees, while maintaining security and decentralization.

### How Does It Work?

The GMX-Solana system primarily consists of on-chain programs and off-chain keepers, along with price and risk oracles. User market operations are generally executed in two steps: first, users submit on-chain transactions to create market operation requests; then, keepers monitor the network, submit the necessary price updates, and finalize the verification and execution of these requests via additional on-chain transactions. Protocol security is ensured by oracle-provided data and on-chain program logic that validates both user requests and keeper actions, supplemented by mechanisms such as price impacts (to mitigate price manipulation risk and maintain pool and open interest balance) and adaptive funding fees (to ensure long-term balance in open interest).

The core market operations include:

- **Deposits and withdrawals to market pools:** Liquidity providers (LPs) contribute liquidity to a market pool by depositing long or short tokens and receive market tokens representing their share of the pool. LPs can redeem market tokens at any time to withdraw their proportional share of assets.

- **Opening and closing perpetual positions:** Traders post collateral to open positions against the market pool's index. When closing a position, profits are withdrawn from the market pool based on index price movement, while losses are deducted from the trader's collateral. The deducted collateral is then deposited into the market pools to cover counterparty profits and maintain liquidity.

- **Swapping assets:** Traders can swap long tokens for short tokens (or vice versa) within the market pools.

LPs primarily earn revenue from order fees and borrowing fees paid by traders when opening or closing positions, or when swapping assets. Traders can also earn by helping maintain market balance, receiving positive price impacts and funding fees paid by the side that increases the imbalance in open interest or the liquidity pool.

### Further Technical Resources & Links

- **GMX-Solana Docs**: Our system documentation, subject to change: https://docs.gmxsol.io
- **GMX-Solana Website**: https://gmxsol.io
- **Twitter**: [@GMX_SOL](https://x.com/GMX_SOL)
- **Discord**: [GMX-Solana](https://discord.gg/gmxsol)

# Scope & Severity Criteria

| Severity level | Impact: High	| Impact: Medium | Impact: Low
|------|-------| -------------- |-------------- |
| Likelihood: High	 | Critical | High | Low |
| Likelihood: Medium | High | Medium | Low |
| Likelihood: Low    | Medium | Low | - |

## Smart Contracts in Scope

**Source**: https://github.com/gmsol-labs/gmx-solana

| Name (Address Link) | Repo |
|------|-------|
| [Store](https://explorer.solana.com/address/Gmso1uvJnLbawvw7yezdfCDcPydwW2s2iqG3w6MDucLo) | github.com/gmsol-labs/gmx-solana/programs/store |
| [Treasury](https://explorer.solana.com/address/GTuvYD5SxkTq4FLG6JV1FQ5dkczr1AfgDcBHaFsBdtBg) | github.com/gmsol-labs/gmx-solana/programs/treasury |
| [Timelock](https://explorer.solana.com/address/TimeBQ7gQyWyQMD3bTteAdy7hTVDNWSwELdSVZHfSXL) | github.com/gmsol-labs/gmx-solana/programs/timelock | 
| [Competition](https://explorer.solana.com/address/2AxuNr6euZPKQbTwNsLBjzFTZFAevA85F4PW9m9Dv8pc) | github.com/gmsol-labs/gmx-solana/programs/competition | 

## Out-of-Scope

### Known Issues

Bug reports covering previously-discovered bugs (listed below) are not eligible for a reward within this program. This includes known issues that the project is aware of but has consciously decided not to “fix”, necessary code changes, or any implemented operational mitigating procedures that can lessen potential risk. Every issue opened in the repo, closed PRs, previous contests and audits are out of scope.

- https://github.com/gmsol-labs/gmx-solana/blob/main/README.md#known-issues

### Previous Audits

Any **previously reported** vulnerabilities mentioned in past audit reports are not eligible for a reward.

GMX-Solana previous audits can be found below:

- https://github.com/gmsol-labs/gmx-solana-audits

### Specific Types of Issues

- Informational findings.
- Design choices or expected design behaviors related to protocol.
- Issues that are ultimately user errors and can easily be caught in the frontend. For example, transfers to the System Program.
- Rounding errors.
- Relatively high gas consumption.
- Attacks requiring access to Timelock or Oracles.
- Risk of loss due to decline in pool asset prices.
- Price manipulation on third-party exchanges.
- Exploits based on delayed or extreme price feed updates.
- Attacks that are not economically feasible.
- Vulnerabilities related to hosting providers. 

# Additional Context

### Trusted Roles

- Program upgrade authorities responsible for deploying and upgrading program code.
- The administrators with control over the default store account authority, typically protected by multisig and timelock mechanisms.
- Any program-defined privileged roles granted or managed by the administrators.
- Keeper accounts responsible for critical operations or maintaining service availability.
