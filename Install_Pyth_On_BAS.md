# Install pyth on BAS with Truffle



## Overview 

In this article, I am going to use Truffle to install a pyth contract on BAS(Biance Application Sidechain) to demonstrate how a smart contract can be deployed to BAS.

## How DApp is developed 

Review the diagram below.

![Image 18-06-2022 at 19.06](/Users/huizhao/Downloads/Image 18-06-2022 at 19.06.jpeg)

### Programming Language 

Solidity, it is a contract oriented programming language that can allow developers to define the business logic. After coding is done, you need to compile the solidity to the smart contract binary code that is to be deployed to EVM through a Node. 

### Truffle

Truffle is a development environment utilizing the [EVM (Ethereum Virtual Machine)](https://moralis.io/introducing-the-moralis-big-evm-update-version-0-0-221/?utm_source=blog&utm_medium=post&utm_campaign=Truffle%20Explained%20%E2%80%93%20What%20is%20the%20Truffle%20Suite%3F) as a basis. The slogan of Truffle is ”Smart Contracts Made Sweeter”, indicating that the environment specializes in [smart contract](https://moralis.io/smart-contracts-explained-what-are-smart-contracts/?utm_source=blog&utm_medium=post&utm_campaign=Truffle%20Explained%20%E2%80%93%20What%20is%20the%20Truffle%20Suite%3F) development. This environment features a number of great functionalities that help dApp developers tremendously. 

- **Smart Contract Management** — This means that Truffle helps manage the artifacts of all smart contracts utilized in your dApps. As Truffle takes care of this, you can focus on other parts of the development process. This further means that Truffle supports library linking, custom deployments, and more complex Ethereum dApps. 
- **Automated Contract Testing** — Another helpful feature of Truffle is that it supports automated contract testing. This means that you can bring your developer experience to the 21st century and construct automated tests for all your contracts. The main benefit of this is that you can shorten the development process of your smart contracts. 
- **Scriptable Migration and Deployment** — With Truffle, you can write deployment scripts that allow you to account for the fact that your dApps will change over time. This means that you can maintain your smart contracts far into the future and in the long term. 
- **Network Management** — Truffle helps you take care of your network by managing your artifacts, allowing you to focus your attention on other tasks.
- **Interactive Console** — Truffle features an interactive console that allows you to access all Truffle commands and contracts you have built. 



### Migration and Deployment Scripts Network Configuration

```json
my_bas_testnet: {
      provider: () => new HDWalletProvider(
          process.env.MNEMONIC,
          "https://bas-aries-public.nodereal.io"
      ),
      confirmations: 10,
      networkCheckTimeout: 1000000,
      timeoutBlocks: 1000,
      skipDryRun: true,
      network_id: 117,
    },
  },
```

#### Concepts

##### MNEMONIC(Secret Phrase)

The secret phrase is **a passphrase created by the user that protects the encryption keys used to encrypt your private keys**.(Never share your secrete phrase to anyone!!!!)

![img](https://d33v4339jhl8k0.cloudfront.net/docs/assets/59907929042863033a1bf144/images/626b4490a535c33d541a320e/file-6cYpLt03s4.png)

##### Node RPC URL

The connection string of your node service. In our example, it is "https://bas-aries-public.nodereal.io".

##### Network ID and Chain ID

Peer-to-peer communication between nodes uses the *network ID*, while the transaction signature process uses the *chain ID*.

| Network   | Chain | Chain ID | Network ID | Type        |
| :-------- | :---- | :------- | :--------- | :---------- |
| `mainnet` | ETH   | 1        | 1          | Production  |
| `ropsten` | ETH   | 3        | 3          | Test        |
| `rinkeby` | ETH   | 4        | 4          | Test        |
| `goerli`  | ETH   | 5        | 5          | Test        |
| `dev`     | ETH   | 2018     | 2018       | Development |
| `classic` | ETC   | 61       | 1          | Production  |
| `mordor`  | ETC   | 63       | 7          | Test        |
| `kotti`   | ETC   | 6        | 6          | Test        |
| `astor`   | ETC   | 212      | 212        | Test        |



#### Steps to Deploy

```shell
# Load the configuration environment variables for deploying your network. make sure to use right env file.
# If it is a new chain you are deploying to, create a new env file and commit it to the repo.
rm -f .env; ln -s .env.prod.xyz .env && set -o allexport && source .env set && set +o allexport

# The Secret Recovery Phrase for the wallet the contract will be deployed from.
export MNEMONIC=...

# Ensure that we deploy a fresh build with up-to-date dependencies.
rm -rf build && npx truffle compile --all

# Merge the network addresses into the artifacts, if some contracts are already deployed.
npx apply-registry

# Perform the migration
npx truffle migrate --network $MIGRATIONS_NETWORK

# Perform this in first time mainnet deployments with Wormhole Receiver. (Or when guardian sets are upgraded)
npm run receiver-submit-guardian-sets -- --network $MIGRATIONS_NETWORK

```

```shell
 npx truffle migrate --network $MIGRATIONS_NETWORK


Compiling your contracts...
===========================
> Everything is up to date, there is nothing to compile.


Starting migrations...
======================
> Network name:    'my_bas_testnet'
> Network id:      117
> Block gas limit: 30000000 (0x1c9c380)


3_deploy_pyth.js
================
pyth2WormholeEmitter: 0xf346195ac02f37d60d4db8ffa6ef74cb1be3550047543a4a9ee9acf4d78697b0
pyth2WormholeChainId: 0x1

   Deploying 'ERC1967Proxy'
   ------------------------
   > transaction hash:    0xf328102095954f2c077f1027c92023c3a20db368f679b3fdeb59ca1f00a3b1fd
   > Blocks: 3            Seconds: 9
   > contract address:    0x147BC67a10a6d77C6Fd97a19033F64eC7d80B105
   > block number:        1415826
   > block timestamp:     1655479010
   > account:             0xf37ef72904d77F17Ca4DEbD1Bb9330e713bE3Df7
   > balance:             62.491351971
   > gas used:            338296 (0x52978)
   > gas price:           1 gwei
   > value sent:          0 ETH
   > total cost:          0.000338296 ETH

   Pausing for 10 confirmations...

   --------------------------------
   > confirmation number: 2 (block: 1415829)
   > confirmation number: 3 (block: 1415830)
   > confirmation number: 5 (block: 1415832)
   > confirmation number: 6 (block: 1415833)
   > confirmation number: 7 (block: 1415834)
   > confirmation number: 9 (block: 1415836)
   > confirmation number: 10 (block: 1415837)
   > Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:         0.000338296 ETH

Summary
=======
> Total deployments:   1
> Final cost:          0.000338296 ETH


```

