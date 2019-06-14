---
title: Truffle | Working With Pantheon
layout: docs.hbs
---
# Working With Pantheon
Truffle supports development with Pantheon, an enterprise oriented Ethereum client
able to work with Ethereum mainnet and private chains.

**Pantheon can create private blockchains with
permissioning and authentication, use different consensus algorithms
(PoW, Clique, IBFT2.0), create private transactions and use privacy groups, and
much more.**

Developing for Pantheon using Truffle is the same as using Truffle to develop
for the public Ethereum networks. Truffle supports Pantheon with the only
difference being Pantheon does not implement private key management.
To use Pantheon with Truffle, you must configure a Truffle wallet.

## Configuration of Truffle wallet
To use Pantheon with Truffle, you must modify your network in `truffle-config.js`.

For security reasons, Pantheon doesn't provide private key and account management.
You have to use a wallet provider to make Truffle able to sign transactions and
configure the wallet provider with a private key of the account to use for your
development process.

1. Install the `truffle-hdwallet-provider` dependency:

```bash
npm install --save truffle-hdwallet-provider@web3-one
```

2. Modify `truffle-config.js`.

See the following example:

```javascript
const PrivateKeyProvider = require("truffle-hdwallet-provider");
const privateKey = "<account-private-key>";
const privateKeyProvider = new PrivateKeyProvider(privateKey, "<JSON-RPC-http-endpoint>");

module.exports = {
  // See <http://truffleframework.com/docs/advanced/configuration>
  // for more about customizing your Truffle configuration!
  networks: {
    pantheonWallet: {
      provider: privateKeyProvider,
      network_id: "*"
    },
  }
};
```
Replace `<account-private-key>` by your private key hexadecimal string and
`<JSON-RPC-http-endpoint>` by the endpoint provided by your pantheon node, usually
`http://localhost:8545`.

## Running Pantheon node
Using Pantheon with Truffle requires that you enable Pantheon JSON-RPC API on the
endpoint that you configured in Truffle.

Depending on your goal - mainnet or private network, with or without privacy -
you will find the best way to run Pantheon on the [Pantheon documentation "Getting
Started" page.](https://docs.pantheon.pegasys.tech/en/stable/Getting-Started/Getting-Started/)

## Using Truffle commands
To deploy a contract on Pantheon network using Truffle, run :

```bash
truffle migrate --network pantheonWallet
```

## More about Pantheon and Truffle
To have more examples of using Pantheon with Truffle, you can read [how to
use Pantheon with Truffle in Pantheon doc](https://docs.pantheon.pegasys.tech/en/stable/Using-Pantheon/Truffle/)
or read about [using Pantheon and Truffle with a free gas network](https://docs.pantheon.pegasys.tech/en/stable/Configuring-Pantheon/FreeGas/#configuring-truffle-for-free-gas) or follow the [Pantheon Quickstart Tutorial](https://docs.pantheon.pegasys.tech/en/stable/Tutorials/Private-Network-Quickstart/) that includes a part about how to run Truffle Pet Shop tutorial.
