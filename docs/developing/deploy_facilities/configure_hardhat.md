---
title: 'Configure Hardhat'
proofedDate: na
iterationBy: na
includedInSite: true
approvedBy: na
comment:
---

Hardhat is a development environment used to compile, deploy, test, and debug Ethereum software. It helps developers manage and automate the recurring tasks that are inherent to the process of building smart contracts and launching dApps, as well as supporting various add-on functionality and features in order to streamline this workflow.

Details on how to use the Hardhat framework will not be described here. You can find all necessary information by reading the [Hardhat documentation](https://hardhat.org/getting-started/#overview).

For a tutorial on how to use Hardhat to deploy on the Neon EVM, see [here](/docs/developing/deploy_facilities/using_hardhat).

## Prerequisites

Before you start, make sure the following software is installed on your device:

- `NodeJS v8.9.4` or later
- `Web3 v1.2.0` or later

Also make sure that the following is true:

- MetaMask is installed on your device. To install MetaMask, follow [this guide](wallet/metamask_setup.md#installing-metamask).
- MetaMask is configured for the Neon EVM.

## Network Configurations

- [Solana cluster](https://docs.solana.com/clusters) is accessed via a proxy.
- Solana works in test mode and the proxy interacts with it through Neon EVM.

## Configure .env file

Before configuring the Hardhat configuration file, make a .env file at the root of your project directory:

```js
PRIVATE_KEY_OWNER=0x.....
```

## The Hardhat Configuration File

To deploy a contract to the Neon EVM with Hardhat, some Neon-specific information must be specified in a configuration file. This configuration file is called `hardhat.config.js` and is located at the root of your project directory. This file is a JavaScript file and can execute any code necessary to create your configuration. Its file schema, variables, and other documentation can be found on the [official Hardhat website](https://hardhat.org/hardhat-runner/docs/config). Please note that the deployer wallet address needs to have enough NEON tokens to cover the gas cost of the deployment. NEON tokens for Devnet can be obtained using the [NeonFaucet](developing/utilities/faucet.md).

The following is a full example, configured for the example below, of the `hardhat.config.js` configuration file for connecting Hardhat to a devnet-proxy using the one-way library on Node.js:

##### hardhat.config.js

```js
require('@nomicfoundation/hardhat-toolbox');
require('dotenv').config();

/** @type import('hardhat/config').HardhatUserConfig */
module.exports = {
  solidity: '0.8.21',
  etherscan: {
    apiKey: {
      neonevm: 'test'
    },
    customChains: [
      {
        network: 'neonevm',
        chainId: 245022926,
        urls: {
          apiURL: 'https://devnet-api.neonscan.org/hardhat/verify',
          browserURL: 'https://devnet.neonscan.org'
        }
      },
      {
        network: 'neonevm',
        chainId: 245022934,
        urls: {
          apiURL: 'https://api.neonscan.org/hardhat/verify',
          browserURL: 'https://neonscan.org'
        }
      }
    ]
  },
  networks: {
    neondevnet: {
      url: 'https://devnet.neonevm.org',
      accounts: [process.env.PRIVATE_KEY_OWNER],
      chainId: 245022926,
      allowUnlimitedContractSize: false,
      gas: 'auto',
      gasPrice: 'auto',
      isFork: true
    },
    neonmainnet: {
      url: 'https://neon-proxy-mainnet.solana.p2p.org',
      accounts: [process.env.PRIVATE_KEY_OWNER],
      chainId: 245022934,
      allowUnlimitedContractSize: false,
      gas: 'auto',
      gasPrice: 'auto',
      isFork: true
    }
  }
};
```

Note that `url` and `chainId` can be retrieved from the RPC endpoints table and/or [chainlist.org](https://chainlist.org/).
