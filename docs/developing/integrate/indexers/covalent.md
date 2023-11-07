---
title: Covalent
proofedDate: na
iterationBy: na
includedInSite: true
approvedBy: na
comment: na
---

## Introduction

[The Covalent Network](https://www.covalenthq.com) is an indexer that provides long-term data availability, providing developers unfettered access to historical blockchain data.

This guide lays out a step-by-step process to configure HTML dApp on Neon EVM using Covalent's SDK.

[View in GitHub](https://github.com/neonlabsorg/neon-tutorials/tree/main/covalent)

### Step 1: Installation
Using Git, clone the example Covalent project from the remote repository and navigate to it:
```sh
git clone https://github.com/neonlabsorg/neon-tutorials
cd neon-tutorials/covalent
```

Now download the project dependencies:
```sh
npm install
```

### Step 2: Generate Covalent's API key
To be able to use Covalent's SDK first you need to generate API key. Head to [Covalent's website](https://www.covalenthq.com) to make an account and generate your API key.

Next thing to do is make a copy of `.env.local.example` file and rename it to `.env.local`. Place your Covalent API key there.

### Step 3: Run
After installing next thing to do is to run the script:
```sh
npm run dev
```

This will start a local web server on your end and in the terminal console you will see the link pointing to it. Open the link in your browser and open the web console. As you can see in the web console we've run the following two sample requests to Covalent SDK:

```javascript
await client.SecurityService.getApprovals(CHAIN, ADDRESS);
```
`getApprovals` method from Covalent's SDK give us the information for all of the on-chain token approvals that specific wallet has ever made. This is a very helpful information when we want to keep safe track of our approvals.

```javascript
await client.BalanceService.getTokenBalancesForWalletAddress(CHAIN, ADDRESS);
```
`getTokenBalancesForWalletAddress` method from Covalent's SDK give us the information for all of tokens *( native, fungible, and non-fungible )* helf by specific wallet address. The response includes spot prices and other metadata.

If you want to query data from [Neon Devnet](https://chainlist.org/?search=Neon+EVM+DevNet&testnets=true) set variable `CHAIN` to `neon-testnet` inside file `main.js`.

More info about other Covalent's SDK methods can be found at their [dependency docs](https://www.npmjs.com/package/@covalenthq/client-sdk).