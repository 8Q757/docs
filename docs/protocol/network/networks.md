---
id: networks
title: NEAR Networks
sidebar_label: Networks
description: "Overview of NEAR Protocol networks including mainnet, testnet, and localnet environments, their purposes, and how to interact with each network."
---

NEAR Protocol operates on several networks, each with its own independent validators and unique state. These networks are designed to serve different purposes, from production-ready applications to testing and development environments.

## Overview of NEAR Networks

- [`mainnet`](/protocol/network/networks#mainnet)
- [`testnet`](/protocol/network/networks#testnet)
- [`localnet`](/protocol/network/networks#localnet)

## Mainnet {#mainnet}

`mainnet` is for production ready smart contracts and live token transfers. Contracts ready for `mainnet` should have gone through rigorous testing and independent security reviews if necessary. `mainnet` is the only network where state is guaranteed to persist over time _(subject to the typical security guarantees of the network's validation process)_.

- Status: `https://rpc.mainnet.near.org/status`
- [ [NearBlocks Explorer](https://nearblocks.io) ]
- [ [Wallet](https://wallet.near.org) ]
- [ [Epoch Sync](https://near-nodes.io/intro/node-epoch-sync) ]

## Testnet {#testnet}

`testnet` is a public network and the final testing network for `nearcore` changes before deployment to `mainnet`. `testnet` is intended for testing all aspects of the NEAR platform prior to `mainnet` deployment. From account creation, mock token transfers, development tooling, and smart contract development, the `testnet` environment closely resembles `mainnet` behavior. All `nearcore` changes are deployed as release candidates on first testnet, before the changes are released on `mainnet`. A number of `testnet` validators validate transactions and create new blocks. dApp developers deploy their applications on `testnet` before deploying on `mainnet`. It is important to note that `testnet` has its own transactions and states.

- Status: `https://rpc.testnet.near.org/status`
- [ [Explorer](https://testnet.nearblocks.io) ]
- [ [Wallet](https://testnet.mynearwallet.com/) ]
- [ [Epoch Sync](https://near-nodes.io/intro/node-epoch-sync) ]

## Localnet {#localnet}

`localnet` is intended for developers who want to work with the NEAR platform independent of the public blockchain. You will need to generate nodes yourself. `localnet` gives you the total control over accounts, economics, and other factors for more advanced use cases (including making changes to `nearcore`). For developers, `localnet` is the right choice if you prefer to avoid leaking information about your work during the development process.

More on local development [here](https://near-nodes.io/validator/running-a-node)


---

:::tip Got a question?
<a href="https://stackoverflow.com/questions/tagged/nearprotocol" target="_blank" rel="noopener noreferrer">
<h8>Ask it on StackOverflow!</h8>
</a>
:::
