---
description: A technical guide for dYdX Chain proposal submission.
---

# Proposal Submission Technical Guide

## Overview

The following are the steps required to be able to submit a proposal using the Command Line Interface (CLI) as laid out on [Step 4 of the Proposal Lifecycle](proposal-lifecycle.md#4.-on-chain-submitting-a-proposal).

## 1. Obtain a \`protocold\` Binary

Before you can submit any `dydxprotocold` command on the CLI, you will need to compile the `protocold` binary locally. This dYdX Protocol's [documentation](https://github.com/dydxprotocol/v4-chain/tree/main/protocol#readme) provides complete instructions on how to compile `protocold` binary locally. Alternatively, if your platform is supported by the prebuilt binaries found in the [releases section](https://github.com/dydxprotocol/v4-chain/releases) of the repository, you can opt to download and use these binaries directly.

## 2. Save your Chain ID in \`dydxprotocold\` Config

To avoid manually passing in the `chain-id` flag for every CLI command, you will need to save it by entering the following command:

```
dydxprotocold config chain-id <chain_id>
```

The `chain-id` for dYdX Chain Mainnet is `dydx-mainnet-1`.

## 3. Confirming Connectivity

To ensure that you are successfully connected to the network, you can test by executing the command below:

```
dydxprotocold status --node https://<RPC ENDPOINT>:443
```

You may replace `<RPC ENDPOINT>` with any of the RPC endpoints listed [here](https://docs.dydx.trade/networks/network1/resources). Remember to append `:443` to the end of the RPC URI to access the endpoint properly and securely.&#x20;

## 4. Registering an Account in the Keychain

When submitting the proposal on dYdX Chain, you will need to add an account in the keychain from which you will submit the proposal. To do this step, you must already have a dYdX Chain wallet and have access to its secret phrase.

* Enter the following command:

```bash
dydxprotocold keys add <KEY NAME> --recover
```

Choose a unique key name to replace `<KEY NAME>`. This name will be used to identify your key within the Keychain.

* Input your secret phrase into the terminal when prompted.

Once you have set up the technical requirements above, you can [create the `json` file](proposal-lifecycle.md#3.-off-chain-dip-creation) and proceed with [submitting the proposal](proposal-lifecycle.md#4.-on-chain-submitting-a-proposal).
