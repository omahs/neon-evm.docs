---
title: Covalent
proofedDate: 20231109
iterationBy: na
includedInSite: true
approvedBy: na
comment: na
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

## TL;DR

- Covalent supports [Neon EVM](https://www.covalenthq.com/docs/networks/neon/)
- [API key required](https://www.covalenthq.com/platform/auth/register/)
- [Tutorial in GitHub](https://github.com/neonlabsorg/neon-tutorials/tree/main/covalent)

## Introduction

[The Covalent Network](https://www.covalenthq.com) is an indexer that provides long-term data availability, providing developers unfettered access to historical blockchain data.

This guide lays out a step-by-step process to configure an HTML dApp on Neon EVM using Covalent's SDK.

### Step 1: Installation

1.1 Clone the example Covalent project from the remote repository and navigate to it:
```bash
git clone https://github.com/neonlabsorg/neon-tutorials
cd neon-tutorials/covalent
```

1.2 Download the project dependencies:
```bash
npm install
```

### Step 2: Generate Covalent's API key

2.1 To use Covalent's SDK, you need to generate an API key. Register with [Covalent](https://www.covalenthq.com/platform/auth/register/) to make an account and generate your key.

2.2 Next, make a copy of `.env.local.example` file and rename it to `.env.local`. Place your Covalent API key there.

### Step 3: Select network

<Tabs>
	<TabItem value="Opt1" label="Mainnet" default>

If you want to query data from [Neon Mainnet](https://chainlist.org/?search=Neon+EVM+MainNet), set variable `CHAIN` to `neon-mainnet` inside the file `main.js`.


</TabItem>
<TabItem value="Opt2" label="Devnet" default>

If you want to query data from [Neon Devnet](https://chainlist.org/?search=Neon+EVM+DevNet&testnets=true), set variable `CHAIN` to `neon-testnet` inside the file `main.js`.

</TabItem>
</Tabs>

### Step 4: Run

3.1 Run the installed script:
```sh
npm run dev
```

This starts a local web server, displaying the server address in the terminal console. Open the link in your browser and open the web console to find the following two sample requests setup in the Covalent SDK:

#### getApprovals

```javascript
await client.SecurityService.getApprovals(CHAIN, ADDRESS);
```
`getApprovals` method from Covalent's SDK gives us the information for all the on-chain token approvals that a specific wallet has ever made.

#### getTokenBalancesForWalletAddress

```javascript
await client.BalanceService.getTokenBalancesForWalletAddress(CHAIN, ADDRESS);
```
`getTokenBalancesForWalletAddress` method from Covalent's SDK provides the information for all tokens *( native, fungible, and non-fungible )* held by a specific wallet address. The response includes spot prices and other metadata.

## What next?

Find more info about Covalent's SDK methods in their [docs](https://www.npmjs.com/package/@covalenthq/client-sdk).