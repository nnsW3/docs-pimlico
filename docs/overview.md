---
sidebar_position: 1
---

# Overview

# Account Abstraction
Account abstraction is a feature that allows users to customize their Ethereum accounts with smart contract logic. It simplifies the account system by reducing Ethereum’s two types of accounts (Externally Owned Accounts and Contract Accounts) to a single type - Contract Accounts. The resulting contract accounts will be able to initiate transactions, pay transaction fees, and have more flexibility and security than regular accounts.

## Why is account abstraction important?
Account abstraction is important for several reasons:

- It enables users to create **smart contract wallets** that can have features such as multisig, social recovery, meta-transactions, batched transactions, gas abstraction, etc.
- It allows users to **pay transaction fees with any token or asset** they want, not just ETH. This can lower the barriers of entry for new users and increase the adoption of Ethereum.
- It gives developers more **freedom and creativity** to design their own account logic and user experience **without being constrained by the protocol rules**. This can foster innovation and diversity in the Ethereum ecosystem.

## How does account abstraction work?
Account abstraction works by allowing contract accounts to specify their own validation logic instead of relying on the protocol’s signature verification and nonce incrementing. This means that contract accounts can decide how to authorize transactions, how to pay for gas fees, and how to prevent replay attacks using smart contract code.

The leading proposal for account abstraction is [ERC-4337](https://eips.ethereum.org/EIPS/eip-4337). ERC-4337 is a specification that aims to use an entry point contract to achieve account abstraction without changing the consensus layer protocol of Ethereum. ERC-4337 simplifies the stack by modularizing the responsibilities of executing the transaction into several entities. 

The different entities that make up ERC-4337 are:
- **Bundlers**: entities that collect UserOperations from users and submit them to an EntryPoint contract.
- **EntryPoint**: a contract that receives UserOperations from bundlers, validates them, pays for gas, and executes them.
- **UserOperations**: pseudo-transaction objects that are used to execute transactions with contract accounts. They contain information such as nonce, gas limit, gas price, initCode or target, data, signature, etc.
- **Wallets**: smart contract accounts that can execute transactions with UserOperations. They have logic to verify signatures, update nonces, and perform actions.
- **Paymasters**: contracts that pay for the gas fees of UserOperations on behalf of wallets. They can implement various payment schemes such as tokens, subscriptions, etc.

For a user-friendly explanation of account abstraction, ERC-4337, and smart contract wallets, we recommend the below video by Kristof Gazso, co-author of ERC-4337 and founder of Pimlico:
<iframe width="560" height="315"
src="https://www.youtube.com/embed/LdaoBzwHFkU" 
frameborder="0" 
allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" 
allowfullscreen></iframe>

## How does Pimlico fit in?

While all of the benefits of account abstraction are already *theoretically* available, there is a major lack of infrastructure available to support this new generation of wallets. 

Pimlico's vision is to be the underlying infrastructure layer that will power Ethereum's transition to smart contract wallets through mass ERC-4337 adoption. 

We will initially be focusing on providing comprehensive infrastructure for two of the above-mentioned entities: **Bundlers and Paymasters**, two of the most critical pieces of the puzzle that are missing for wallets building on top of ERC-4337.