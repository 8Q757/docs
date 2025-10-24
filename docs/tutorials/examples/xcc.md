---
id: xcc
title: Cross Contract Call
description: "Learn how to perform a basic cross-contract call on NEAR to set and retrieve greetings."
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';
import {CodeTabs, Language, Github} from '@site/src/components/UI/Codetabs'
import MovingForwardSupportSection from '@site/src/components/MovingForwardSupportSection';

This example performs the simplest cross-contract call possible: it calls our [Hello NEAR](https://github.com/near-examples/hello-near-examples) example to set and retrieve a greeting.
It is one of the simplest examples on making a cross-contract call, and the perfect gateway to the world of interoperative contracts.

:::info Advanced Cross-Contract Calls
Check the tutorial on how to perform cross-contract calls [in batches and in parallel](./advanced-xcc)
:::

---

## Clone the Example

You have two options to start the project:

1. You can use the app through `Github Codespaces`, which will open a web-based interactive environment.
2. Clone the repository locally and use it from your computer.

| Codespaces                                                                                                                                      | Clone locally                                              |
| ----------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| [![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/near-examples/cross-contract-calls?quickstart=1) | 🌐 `https://github.com/near-examples/cross-contract-calls` |

---

## Structure of the Example

The smart contract is available in two flavors: Rust and JavaScript

<Tabs groupId="code-tabs">

  <TabItem value="js" label="🌐 JavaScript">

```bash
┌── sandbox-ts # sandbox testing
│    ├── hello-near
│    │    └── hello-near.wasm
│    └── main.ava.ts
├── src # contract's code
│    └── contract.ts
├── package.json
├── README.md
└── tsconfig.json
```

  </TabItem>

  <TabItem value="rust" label="🦀 Rust">

```bash
┌── tests # sandbox testing
│    ├── hello-near
│    │    └── hello-near.wasm
│    └── tests.rs
├── src # contract's code
│    ├── external.rs
│    └── lib.rs
├── Cargo.toml # package manager
├── README.md
└── rust-toolchain.toml
```

  </TabItem>

</Tabs>

---

## Smart Contract

The contract exposes methods to query the greeting and change it. These methods do nothing but calling `get_greeting` and `set_greeting` in the `hello-near` example.

<hr class="subsection" />

### Querying for the Greeting

The contract performs a cross-contract call to `hello.near-example.testnet` to get the greeting message, and then handles the response in a **callback function**.

<Tabs>
  <TabItem value="js" label="🌐 JavaScript">
    <Github fname="contract.ts" language="ts"
            url="https://github.com/near-examples/cross-contract-calls/blob/main/contract-simple-ts/src/contract.ts#L25-L40"
            start="25" end="40" />
  </TabItem>
  <TabItem value="rust" label="🦀 Rust (low level)">
    <Github fname="lib.rs" language="rust"
            url="https://github.com/near-examples/cross-contract-calls/blob/main/contract-simple-rs/src/low_level.rs#L6-L23"
            start="6" end="23" />
  </TabItem>
  <TabItem value="rust-hl" label="🦀 Rust (high level)">
    <Github fname="external.rs" language="rust"
      url="https://github.com/near-examples/cross-contract-calls/blob/main/contract-simple-rs/src/high_level.rs#L9-L21"
      start="9" end="21" />

    Which requires you to define the external contract interface:

    <Github fname="external.rs" language="rust"
      url="https://github.com/near-examples/cross-contract-calls/blob/main/contract-simple-rs/src/external_contract.rs"
      start="4" end="12" />
  </TabItem>
</Tabs>

<hr class="subsection" />

### Callback Function

The callback function processes the result of the cross-contract call. In this case, it simply returns the greeting message obtained from the `hello-near` contract.

Notice that the callback function is marked as **private**, meaning it can only be called by the contract itself.

<Tabs>
  <TabItem value="js" label="🌐 JavaScript">
    <Github fname="contract.ts" language="ts"
      url="https://github.com/near-examples/cross-contract-calls/blob/main/contract-simple-ts/src/contract.ts#L42-L52"
      start="42" end="52" />
  </TabItem>
  <TabItem value="rust" label="🦀 Rust">
    <Github fname="lib.rs" language="rust"
            url="https://github.com/near-examples/cross-contract-calls/blob/main/contract-simple-rs/src/low_level.rs#L25-L39"
            start="25" end="39" />
  </TabItem>
</Tabs>

---

## Testing the Contract

The contract readily includes a set of unit and sandbox testing to validate its functionality. To execute the tests, run the following commands:

<Tabs groupId="code-tabs">
  <TabItem value="js" label="🌐 JavaScript">

  ```bash
  cd contract-simple-ts
  yarn
  yarn test
  ```

  </TabItem>
  <TabItem value="rust" label="🦀 Rust">

  ```bash
  cd contract-simple-rs
  cargo test
  ```
  </TabItem>

</Tabs>

:::tip
The `integration tests` use a sandbox to create NEAR users and simulate interactions with the contract.
:::

In this project in particular, the integration tests first deploy the `hello-near` contract. Then,
they test that the cross-contract call correctly sets and retrieves the message. You will find the integration tests
in `sandbox-ts/` for the JavaScript version and in `tests/` for the Rust version.

<CodeTabs>
  <Language value="js" language="js">
    <Github fname="main.ava.ts"
            url="https://github.com/near-examples/cross-contract-calls/blob/main/contract-simple-ts/sandbox-ts/main.ava.ts"
            start="8" end="52" />
  </Language>
  <Language value="rust" language="rust">
    <Github fname="lib.rs"
            url="https://github.com/near-examples/cross-contract-calls/blob/main/contract-simple-rs/tests/tests.rs"
            start="4" end="77" />
  </Language>
</CodeTabs>


<hr class="subsection" />

### Deploying the Contract to the NEAR network

In order to deploy the contract you will need to create a NEAR account.

<Tabs groupId="cli-tabs">
  <TabItem value="short" label="Short">

  ```bash
  # Create a new account pre-funded by a faucet
  near create-account <accountId> --useFaucet
  ```
  </TabItem>

  <TabItem value="full" label="Full">

  ```bash
  # Create a new account pre-funded by a faucet
  near account create-account sponsor-by-faucet-service <my-new-dev-account>.testnet autogenerate-new-keypair save-to-keychain network-config testnet create
  ```
  </TabItem>
</Tabs>

Go into the directory containing the smart contract (`cd contract-advanced-ts` or `cd contract-advanced-rs`), build and deploy it:

<Tabs groupId="code-tabs">

  <TabItem value="js" label="🌐 JavaScript">

    ```bash
    npm run build
    near deploy <accountId> ./build/cross_contract.wasm --initFunction new --initArgs '{"hello_account":"hello.near-example.testnet"}'
    ```

  </TabItem>
  <TabItem value="rust" label="🦀 Rust">
  
  ```bash
  cargo near deploy build-non-reproducible-wasm <accountId> with-init-call new json-args '{"hello_account":"hello.near-example.testnet"}' prepaid-gas '100.0 Tgas' attached-deposit '0 NEAR' network-config testnet sign-with-keychain send

  ```

  </TabItem>

</Tabs>

<hr class="subsection" />

### CLI: Interacting with the Contract

To interact with the contract through the console, you can use the following commands:

<Tabs groupId="cli-tabs">
  <TabItem value="short" label="Short">

  ```bash
  # Get message from the hello-near contract
  # Replace <accountId> with your account ID
  near call <accountId> query_greeting --accountId <accountId>

  # Set a new message for the hello-near contract
  # Replace <accountId> with your account ID
  near call <accountId> change_greeting '{"new_greeting":"XCC Hi"}' --accountId <accountId>
  ```
  </TabItem>

  <TabItem value="full" label="Full">

  ```bash
  # Get message from the hello-near contract
  # Replace <accountId> with your account ID
  near contract call-function as-transaction <accountId> query_greeting json-args '{}' prepaid-gas '100.0 Tgas' attached-deposit '0 NEAR' sign-as <accountId> network-config testnet sign-with-keychain send

  # Set a new message for the hello-near contract
  # Replace <accountId> with your account ID
  near contract call-function as-transaction <accountId> change_greeting json-args '{"new_greeting":"XCC Hi"}' prepaid-gas '100.0 Tgas' attached-deposit '0 NEAR' sign-as <accountId> network-config testnet sign-with-keychain send
  ```
  </TabItem>
</Tabs>

---

## Moving Forward

A nice way to learn is by trying to expand a contract. Modify the cross contract example to use the [guest-book](guest-book.md)
contract!. In this way, you can try to make a cross-contract call that attaches money. Remember to correctly [handle the callback](/smart-contracts/anatomy/crosscontract#callback-function),
and to return the money to the user in case of error.

### Advanced Cross Contract Calls

Your contract can perform multiple cross-contract calls in simultaneous, creating promises that execute in parallel, or as a batch transaction. Check the [advanced cross contract calls
tutorial](./advanced-xcc) to learn more.

<MovingForwardSupportSection />

:::note Versioning for this article

At the time of this writing, this example works with the following versions:

- near-cli: `4.0.13`
- node: `18.19.1`
- rustc: `1.77.0`

:::
