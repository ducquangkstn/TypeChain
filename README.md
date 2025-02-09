<p align="center">
  <img src="https://github.com/Neufund/TypeChain/blob/d82f3cc644a11e22ca8e42505c16f035e2f2555d/docs/images/typechain-logo.png?raw=true" width="300" alt="TypeChain">
  <h3 align="center">TypeChain</h3>
  <p align="center">🔌 TypeScript bindings for Ethereum smart contracts</p>

  <p align="center">
    <a href="https://github.com/ethereum-ts/TypeChain/actions"><img alt="Build Status" src="https://github.com/ethereum-ts/TypeChain/workflows/CI/badge.svg"></a>
    <img alt="Downloads" src="https://img.shields.io/npm/dm/typechain.svg">
    <a href="/package.json"><img alt="Software License" src="https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square"></a>
  </p>

  <p align="center">
    <i>Used by the best:</i> <br/>
    <img src="https://raw.githubusercontent.com/ethereum-ts/TypeChain/master/docs/images/maker-logo.png" height="110" alt="Maker DAO" />
    <a href="https://github.com/Uniswap/uniswap-v3-core/blob/main/hardhat.config.ts#L1"><img src="https://raw.githubusercontent.com/ethereum-ts/TypeChain/master/docs/images/uniswap-logo.png" height="90" alt="Uniswap" /></a>
    <a href="https://github.com/aave/protocol-v2/blob/master/hardhat.config.ts#L16"><img src="https://raw.githubusercontent.com/ethereum-ts/TypeChain/master/docs/images/aave-logo.png" height="60" alt="AAVE" /></a>
    <br/>
    <a href="https://github.com/ethereum-optimism/optimism/blob/master/packages/contracts/hardhat.config.ts#L14"><img src="https://raw.githubusercontent.com/ethereum-ts/TypeChain/master/docs/images/optimism-logo.png" height="90" alt="Optimism" /></a>
    <a href="https://github.com/matter-labs/zksync/blob/9687049af1efbd14d8e47d97ebea643e1516da9d/contracts/hardhat.config.ts#L4"><img src="https://raw.githubusercontent.com/ethereum-ts/TypeChain/master/docs/images/zksync-logo.png" height="100" alt="zkSync" /></a>
  </p>
</p>

## Features ⚡

- static typing - you will never call not existing method again
- IDE support - works with any IDE supporting Typescript
- extendible - work with many different tools: `ethers.js`, `hardhat`, `truffle`, `Web3.js` or you can create your own
  target
- frictionless - works with simple, JSON ABI files as well as with Truffle/Hardhat artifacts

## Installation

```bash
npm install --save-dev typechain
```

You will also need to install a desired target for example `@typechain/ethers-v4`. [Learn more about targets](#targets-)

## Packages 📦

| Package                                                | Version                                                                                                               | Description                                  | Examples                                                                           |
| ------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------- | -------------------------------------------- | ---------------------------------------------------------------------------------- |
| [`typechain`](/packages/typechain)                     | [![npm](https://img.shields.io/npm/v/typechain.svg)](https://www.npmjs.com/package/typechain)                         | Core package                                 | -                                                                                  |
| [`@typechain/ethers-v5`](/packages/target-ethers-v5)   | [![npm](https://img.shields.io/npm/v/@typechain/ethers-v5.svg)](https://www.npmjs.com/package/@typechain/ethers-v5)   | Ethers ver 5 support (⚠️ requires TS 4.0 >=) | [example](./examples/ethers-v5)                                                    |
| [`@typechain/ethers-v4`](/packages/target-ethers-v4)   | [![npm](https://img.shields.io/npm/v/@typechain/ethers-v4.svg)](https://www.npmjs.com/package/@typechain/ethers-v4)   | Ethers ver 4 support                         | [example](./examples/ethers-v4)                                                    |
| [`@typechain/truffle-v5`](/packages/target-truffle-v5) | [![npm](https://img.shields.io/npm/v/@typechain/truffle-v5.svg)](https://www.npmjs.com/package/@typechain/truffle-v5) | Truffle ver 5 support                        | [example](./examples/truffle-v5)                                                   |
| [`@typechain/truffle-v4`](/packages/target-truffle-v4) | [![npm](https://img.shields.io/npm/v/@typechain/truffle-v4.svg)](https://www.npmjs.com/package/@typechain/truffle-v4) | Truffle ver 4 support                        | [example](./examples/truffle-v4)                                                   |
| [`@typechain/web3-v1`](/packages/target-web3-v1)       | [![npm](https://img.shields.io/npm/v/@typechain/web3-v1.svg)](https://www.npmjs.com/package/@typechain/web3-v1)       | Web3 ver 1 support                           | [example](./examples/web3-v1)                                                      |
| [`@typechain/hardhat`](/packages/hardhat)              | [![npm](https://img.shields.io/npm/v/@typechain/hardhat.svg)](https://www.npmjs.com/package/@typechain/hardhat)       | Hardhat plugin                               | [example-ethers](./examples/hardhat) [example-truffle](./examples/hardhat-truffle) |

## Usage

### CLI

_Note: If you use hardhat just use
[hardhat plugin](https://github.com/ethereum-ts/TypeChain/tree/master/packages/hardhat)._

```
typechain --target=(ethers-v4|ethers-v5|truffle-v4|truffle-v5|web3-v1|path-to-custom-target) [glob]
```

- `glob` - pattern that will be used to find ABIs, remember about adding quotes: `typechain "**/*.json"`, examples:
  `./abis/**/*.abi`, `./abis/?(Oasis.abi|OasisHelper.abi)`.
- `--target` - ethers-v4, ethers-v5, truffle-v4, truffle-v5, web3-v1 or path to your custom target. Typechain will try to load
  package named: `@typechain/${target}`, so make sure that desired package is installed.
- `--out-dir` (optional) - put all generated files to a specific dir.
- `--always-generate-overloads` (optional) - some targets won't generate unnecessary types for overloaded functions by
  default, this option forces to always generate them

TypeChain always will rewrite existing files. You should not commit them. Read more in FAQ section.

Example:

```
typechain --target ethers-v5 --out-dir app/contracts './node_modules/neufund-contracts/build/contracts/*.json'
```

## Videos

- [Devcon5 Video (2019)](https://www.youtube.com/watch?v=Ho4dGNKVkTE)

## Getting started 📚

### Motivation

Interacting with blockchain in Javascript is a pain. Developers need to remember not only a name of a given smart
contract method or event but also it's full signature. This wastes time and might introduce bugs that will be triggered
only in runtime. TypeChain solves these problems (as long as you use TypeScript).

### How does it work?

TypeChain is a code generator - provide ABI file and name of your blockchain access library (ethers/truffle/web3.js) and
you will get TypeScript typings compatible with a given library.

### Step by step guide

Install TypeChain with `yarn add --dev typechain` and install desired target.

Run `typechain --target=your_target` (you might need to make sure that it's available in your path if you installed it
only locally), it will automatically find all `.abi` files in your project and generate Typescript classes based on
them. You can specify your glob pattern: `typechain --target=your_target "**/*.abi.json"`. `node_modules` are always
ignored. We recommend git ignoring these generated files and making typechain part of your build process.

That's it! Now, you can simply import typings, check out our examples for more details.

## Targets 🎯

### Ethers.js v4 / v5

Use `ethers-v5` target to generate wrappers for [ethers.js](https://github.com/ethers-io/ethers.js/) lib. To make it
work great with Hardhat, use [Hardhat plugin](https://github.com/ethereum-ts/TypeChain/tree/master/packages/hardhat).

### Truffle v4 / v5

Truffle target is great when you use truffle contracts already. Check out
[truffle-typechain-example](https://github.com/ethereum-ts/truffle-typechain-example) for more details. It require
installing [typings](https://www.npmjs.com/package/truffle-typings) for truffle library itself.

Now you can simply use your contracts as you did before and get full type safety, yay!

### Web3 v1

Generates typings for contracts compatible with latest stable Web3.js version. Typings for library itself are now part
of the `Web3 1.0.0` library so nothing additional is needed. For now it needs explicit cast as shown
[here](https://github.com/krzkaczor/TypeChain/pull/88/files#diff-540a9b8840419be93ddb8d4b53325637R8), this will be fixed
after improving official typings.

### NatSpec support

If you provide solidity artifacts rather than plain ABIs as an input, TypeChain can generate NatSpec comments directly
to your typings which enables simple access to docs while coding.

### Your own target

This might be useful when you're creating a library for users of your smartcontract and you don't want to lock yourself
into any API provided by Web3 access providing library. You can generate basically any code (even for different
languages than TypeScript!) that based on smartcontract's ABI.

## FAQ 🤔

### Q: Should I commit generated files to my repository?

A: _NO_ — we believe that no generated files should go to git repository. You should git ignore them and make
`typechain` run automatically for example in post install hook in package.json:

```
"postinstall":"typechain"
```

When you update ABI, just regenerate files with TypeChain and Typescript compiler will find any breaking changes for
you.

### Q: How do I customize generated code?

A: You can create your own target and generate basically any code.

### Q: Generated files won't match current codestyle of my project :(

A: We will automatically format generated classes with `prettier` to match your coding preferences (just make sure to
use `.prettierrc` file).

Furthermore, TypeChain will silent `eslint` and `tslint` errors for generated files.

### Usage as API

```typescript
import { runTypeChain, glob } from 'typechain'

async function main() {
  const cwd = process.cwd()
  // find all files matching the glob
  const allFiles = glob(cwd, [`${config.paths.artifacts}/!(build-info)/**/+([a-zA-Z0-9_]).json`])

  const result = await runTypeChain({
    cwd,
    filesToProcess: allFiles,
    allFiles,
    outDir: 'out directory',
    target: 'target name',
  })
}

main().catch(console.error)
```

If you don't care about incremental generation just specify the same set of files for `filesToProcess` and `allFiles`.
For incremental generation example read the source code of
[hardhat plugin](https://github.com/ethereum-ts/TypeChain/blob/master/packages/hardhat/src/index.ts).

# Contributing

Check out our [contributing guidelines](./CONTRIBUTING.md)

# Licence

Kris Kaczor (krzkaczor) MIT | [Github](https://github.com/krzkaczor) | [Twitter](https://twitter.com/krzkaczor)
