# Ethereum Contracts

This directory contains smart contracts utilized by the Polkadot-Ethereum Bridge.

- Bridge.sol: application registry and routing of messages from Substrate
- Application.sol: an abstract contract that must be implemented by any Bridge application
    - ETHApp.sol: application for cross-chain ETH transfers between Ethereum and Substrate
    - ERC20App.sol: application for cross-chain ERC20 transfers between Ethereum and Substrate
- Decoder.sol: a library for decoding SCALE encoded data
- Verifier.sol: verifies tx origin and signatures
- Scale.sol: implements decoding of SCALE encoded compact uints; not currently used, included to support future work on generalized data relay

## Set up

After starting the blockchain and deploying the contracts, the Bridge's Ethereum component is ready for usage.


Install truffle:

```bash
yarn global add truffle
```

Install dependencies with yarn:

```bash
yarn install
```

Set up `.env` file. Note that deploying to ropsten network requires modifying the INFURA_PROJECT_ID and MNEMONIC environment variables.

```bash
cp .env.example .env
```

Start truffle environment containing a local Ethereum network:

```bash
truffle develop
```

Open a fresh terminal window and deploy the contracts:

```bash
truffle migrate --all
```

## Testing

Make sure the truffle environment is running, then run tests

```bash
# Start testing environment if it's not already running
truffle develop

# In a new terminal, test application gas expenditures
truffle test test/test_gas.js

# Run all tests
truffle test
```

## Scripts


The project includes several scripts for Bridge interaction:

`getTx.js` gets information about a transaction

``` bash
truffle exec scripts/getTx.js [tx-hash]
```

`getEthBalance.js` gets an address' ETH balance

``` bash
truffle exec scripts/getEthBalance.js [ethereum-address]
```

`getERC20balance.js` gets an address' ERC20 token balance

``` bash
truffle exec scripts/getERC20Balance.js [ethereum-address] [token-contract-address]
```

`sendEth.js` deposits ETH into the ETHApp, initiating a cross-chain transfer to Substrate

``` bash
truffle exec scripts/sendEth.js [amount] [polkadot-recipient]
```

`sendERC20.js` deposits ERC20 tokens into the ERC20App, initiating a cross-chain transfer to Substrate

``` bash
truffle exec scripts/sendERC20.js [amount] [token-contract-address] [polkadot-recipient]
```


## Autogenerated Documentation

Solidity documentation can be autogenerated using the [solidity-docgen](https://github.com/OpenZeppelin/solidity-docgen) library. It will generate markdown files from the contracts directory and output them to the docs directory.

```bash
# The library is only compatible with npx
npx solidity-docgen
```
