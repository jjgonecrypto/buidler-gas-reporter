[![Build Status](https://travis-ci.org/cgewecke/buidler-gas-reporter.svg?branch=master)](https://travis-ci.org/cgewecke/buidler-gas-reporter)

# buidler-gas-reporter 

[eth-gas-reporter](https://github.com/cgewecke/eth-gas-reporter) plugin for [buidler](http://getbuidler.com). :fuelpump: 

## What

A mocha utility for Ethereum test suites which reports:
+ Gas usage per unit test.
+ Average gas usage per method call / contract deployment.
+ Real-time national currency costs for using and deploying your contract system. :euro:

## Installation

```bash
npm install buidler-gas-reporter --save-dev
```

And add the following to your `buidler.config.js`:

```js
usePlugin("@nomiclabs/buidler-gas-reporter");
```

## Configuration 
Configuration is optional.
```js
module.exports = {
  gasReporter: {
    currency: 'CHF',
    gasPrice: 21
  }
}
```
:bulb: **Pro Tip**

The options include an `enabled` key that lets you toggle gas reporting on and off using shell
environment variables. When `enabled` is false, mocha's (faster) default spec reporter is used.
Example:

```js
module.exports = {
  gasReporter: {
    enabled: (process.env.REPORT_GAS) ? true : false
  }
}
```
## Usage

This plugin overrides the built-in `test` task. Gas reports are generated by default with:
```
npx buidler test
```

## Options
| Option            | Type       | Default                              | Description                                                                                                                                                                               |
| ----------------- | ---------- | ------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| enabled | _Boolean_ | true | Toggle gas reporter on/off. |
| currency          | _String_   | 'EUR'                                | National currency to represent gas costs in. Exchange rates loaded at runtime from the `coinmarketcap` api. Available currency codes can be found [here](https://coinmarketcap.com/api/). |
| gasPrice          | _Number_   | (varies)                             | Denominated in `gwei`. Default is loaded at runtime from the `eth gas station` api                                                                                                        |
| outputFile        | _String_   | stdout                               | File path to write report output to                                                                                                                                                       |
| noColors          | _Boolean_  | false                                | Suppress report color. Useful if you are printing to file b/c terminal colorization corrupts the text.                                                                                    |
| onlyCalledMethods | _Boolean_  | true                                 | Omit methods that are never called from report.                                                                                                                                           |
| rst               | _Boolean_  | false                                | Output with a reStructured text code-block directive. Useful if you want to include report in RTD                                                                                         |
| rstTitle          | _String_   | ""                                   | Title for reStructured text header (See Travis for example output)                                                                                                                        |
| showTimeSpent     | _Boolean_  | false                                | Show the amount of time spent as well as the gas consumed                                                                                                                                 |
| excludeContracts  | _String[]_ | []                                   | Contract names to exclude from report. Ex: `['Migrations']`                                                                                                                               |
| src               | _String_   | "contracts"                          | Folder in root directory to begin search for `.sol` files. This can also be a path to a subfolder relative to the root, e.g. "planets/annares/contracts"                                  |
| url               | _String_   | value of `web3.currentProvider.host` | RPC client url (e.g. "http://localhost:8545"). (For non-buidler / non-truffle projects) |
| proxyResolver | _Function_ | none | Custom method to resolve identity of methods managed by a proxy contract. |
