# COTI Remix Plugin

<p align="center">
  <img src="remix_plugin_cover.jpg" style="width:400px" />
</p>

<p align="center"><a href="https://discord.gg/YdTB3P5P">
  <img src="https://img.shields.io/discord/386571547508473876?label=Discord" />
</a></p>

Welcome to the **COTI Remix Plugin** repository.

The plugin seamlessly integrates with the Remix IDE, enabling developers to deploy and interact with contracts on the COTI network.

> [!NOTE]
> 1. The current version of the Remix plugin supports COTI Devnet only. Testnet support will be added soon.
>
> 2. The COTI Remix Plugin is not yet published natively to Remix. While we publish, follow below steps for local plugin installation.

> [!IMPORTANT]  
> In order to use the privacy-preserving features of the COTI network with the Remix plugin, your workspace must include both [`MpcCore.sol`](https://github.com/coti-io/confidentiality-contracts/blob/main/contracts/lib/MpcCore.sol) and [`MpcInterface.sol`](https://github.com/coti-io/confidentiality-contracts/blob/main/contracts/lib/MpcInterface.sol) files.

## Installation

1. Simply [open Remix](https://remix.ethereum.org/) and click the `Plugin Manager` icon on the lower-left part of the screen. Type "COTI" on the searchbox, once the plugin is visible, click "Activate".

2. **Usage**: Once the plugin is activated, you'll find an easy-to-use interface that allows you to deploy and interact with COTI contracts. Follow the on-screen prompts and tooltips to compile, deploy, and interact with your contracts.

3. **Feedback**: We want your feedback. If you encounter any issues or suggestions, please let us know in the **[#developers](https://discord.gg/YdTB3P5P)** Discord channel.

## Video Overview

<p><a href="https://youtu.be/o59aENKhkAI?si=wkWJ9f15V_oirjTq" target="_blank">
<img src="https://i.ytimg.com/vi/o59aENKhkAI/0.jpg" alt="COTI Remix Plugin Demo">
</a></p>

### Plugin Features

The plugin is comprised of 5 main sections, described below.

### Environment

The environment section (located at the bottom of the plugin) allows you to select the environment you wish to use to connect to the COTI network. Two options are available:

1. **Wallet**: This option uses a browser-based wallet (i.e., MetaMask). You will need to have the COTI network added to your wallet. You may add the COTI network by visiting [Chainlist](https://chainlist.org/?search=coti&testnets=true).

2. **Manual (Devnet)**: This option creates 2 accounts for you in the COTI network. 

Both options are tracked in the `coti_wallet_config.json` file, stored at the root of your workspace.

### 1. Faucet

The Faucet section will display your account balance and provide a link to the [COTI faucet](https://discord.gg/dnRhU2Wb) on Discord. To request funds send a message to the bot using the format: `devnet <address>`, for example:

    devnet 0xDa28f69CbB6d6072DA4bb10378fB87e367c6dF0D

### 2. Onboard

The Onboard section of the plugin provides an easy way to generate an AES key. This AES key will be used for encryption and decryption purposes within the COTI network.

If the account has already been onboarded and an AES key has already been created, the key will be displayed in this section.

The Onboard action makes use of the [AccountOnboard.sol](https://github.com/coti-io/confidentiality-contracts/blob/main/contracts/AccountOnboard/AccountOnboard.sol) smart contract via the Typescript SDK [onboard.ts](https://github.com/coti-io/coti-sdk-typescript/blob/main/src/account/onboard.ts) script.

Once the `Onboard` button is clicked, the plugin will return data related to your AES key. You may clear this data by clicking on the `Clear AES Key` button.

The AES key is stored in the `coti_wallet_config.json` file as `"user_key"`.

### 3. Compile & Deploy

The "Compile & Deploy" section of the plugin serves a similar purpose to the native Remix "Compile" feature, with the key difference that it allows users to compile contracts that are making use of the privacy-preserving features of the COTI network.

Four sub-sections are offered:

- `Compile` section

    - **Compiler version drop-down**: Allows user to select the desired compiler version

    - `Compile` action button: Compiles the contract using the configured compiler version.

    - **Contract selection drop-down**: Allows selection of previously compiled contracts.

- `Deploy` section

    - **Value** (in wei, gwei, or ether): Allows configuration of custom gas amount when the default estimated gas is not used.

    - `Deploy` action button: deploys the indicated contract with the configured parameters.

- `Load From Address` section

    - `Address` input field: Input field to enter the address of a previously deployed contract.

    - `Load Contract` action button: Loads contract indicated on the `Address` field.

### 4. Interact

The "Interact" section of the plugin serves a similar purpose to the native Remix "Interact" feature, with the key difference that it allows users to interact with contracts that are making use of the privacy-preserving features of the COTI network.

## Working with Encrypted Data

The COTI Remix plugin will automatically encrypt/decrypt values of type `IT` (input text) and `CT` (cipher text).

For `IT` (input text) value types, only cleartext is required, the encryption is performed automatically by the plugin.
