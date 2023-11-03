---
title: Deploy with Hardhat
proofedDate: na
iterationBy: na
includedInSite: true
approvedBy: na
comment: 
---

*This page outlines the steps for deploying and testing contracts in the Neon EVM using the Hardhat tool.*

Before beginning the tutorial below, make sure that you have properly [configured Hardhat](configure_hardhat) for the Neon EVM.

## How to Use Hardhat: A Tutorial
The example this tutorial is based on is located in [this repository](https://github.com/neonlabsorg/neon-tutorials).

By the end of this tutorial, you will deploy a contract describing an ERC-20 token to the Neon Devnet. You will then test this contract by transfering tokens to random generated wallet.

### Step 1: Installation
> **Note:** This page is just a quickstart based on a specific example program. For more details on installing Hardhat, refer to the *[Hardhat documentation](https://hardhat.org/hardhat-runner/docs/getting-started#overview)*.

Using Git, clone the example Hardhat project from the remote repository and navigate to it:
```sh
git clone https://github.com/neonlabsorg/neon-tutorials
cd neon-tutorials/hardhat
```

Then, run the following command:
```sh
npm install
```
This will install all the necessary packages to continue with the example. These packages include the `Hardhat` library.

If the above command results in an error, run:
```sh
npm cache clear --force
npm install
```

### Step 2: Set Up Signer Account
To interact with the soon-to-be-deployed contracts, you'll need to create new wallet. For this you can use MetaMask or any other wallet provider.

In MetaMask this can be done by clicking on your current account's icon in the top right of the MetaMask extension pop-up, and then clicking on 'Create an Account' in the drop-down menu that appears. Then, obtain some Devnet NEON tokens for these accounts _(up to 100 NEON per account)_ using the [NeonFaucet](https://neonfaucet.org/) _(without having NEON balance you won't be able to sign and submit transactions)_. 

Last action of this step is to copy the new wallet account private key and paste it into the `.env` file _(copy and rename `.env.example` to `.env` and place the private key there)_. To obtain the private key from MetaMask, click on the three vertical dots to the right of your currently displayed account name and wallet address. In this drop-down menu, click on 'Account Details', then on 'Export Private Key', and enter your password and click 'Confirm' to get access to the private key for that account.

### Step 3: Compile Contracts
All of the contracts are located in the project's `contracts/` directory. Before these contracts can be run, they must first be compiled. To compile the project's contracts, run the following command:
```sh
npx hardhat compile
```

After running this step, you should see output similar to the following:
```
Compiled X Solidity files successfully
```

### Step 4: Deploy Contracts
To deploy the project's contracts, simply run the command below to run the deployment script in the `scripts/` directory:
```sh
npx hardhat run scripts/TestERC20/deploy.js --network neondevnet
```

This command compiles the contracts in the `contracts/` and deploys them to the Neon Devnet. The output should look something like this:
```
TestERC20 token deployed to <CONTRACT_ADDRESS>
```

If you wish to deploy on Neon Mainnet then just switch the `--network` parameter to `neonmainnet`.

### Step 5: Testing Contracts
This step in our example will also initiate transactions on Neon Devnet. Copy the new deployed smart contract address from the previous step and paste it inside file `scripts/TestERC20/transfer.js`. Next run the following command:
```sh
npx hardhat run scripts/TestERC20/transfer.js
```

After running this command, you should see console output similar to the following:
```
Sender balance before transfer 1000000000000000000000n
Receiver balance before transfer 0n
Sender balance after transfer 990000000000000000000n
Receiver balance after transfer 10000000000000000000n
```
Which means that from our signer account we have sent 1000 * 10 ** 18 tokens to random generated wallet address.

### Step 6: Neonscan contract verification
In this step we will verify our freshly deployed smart contract on our explorer Neonscan. This can be done by running the following command:
```sh
npx hardhat verify --network neondevnet <CONTRACT_ADDRESS>
```
You have to replace `<CONTRACT_ADDRESS>` with your smart contract address.

This command will verify our smart contract on our [Devnet Neonscan](https://devnet.neonscan.org), but if you wish to verify a contract on the [Mainnet Neonscan](https://neonscan.org) then you have to change parameter `--network` to `neonmainnet`.


### Step 7: Connect Project to MetaMask
To import your project as an asset in MetaMask, follow the instructions [here](https://support.metamask.io/hc/en-us/articles/360015489031-How-to-add-unlisted-tokens-custom-tokens-in-MetaMask#h_01FWH492CHY60HWPC28RW0872H) and use the contract address from the previous step as the 'Token Contract Address' in MetaMask.

Once you complete this final step, you will be able to see your new ERC-20 assets in the MetaMask profiles of the new test accounts.
```sh
npx hardhat verify --network neondevnet <CONTRACT_ADDRESS>
```