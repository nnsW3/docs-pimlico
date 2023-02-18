---
sidebar_position: 2
---

# API

## eth_canSponsorUserOperation

This function checks whether a UserOperation can be sponsored by the Paymaster service.

### Parameters

- `userOperation`: A UserOperation struct that contains information about the action to be executed through a smart contract account. It has the following fields:
  - `sender`: The address of the sender smart contract account.
  - `nonce`: The nonce of the sender smart contract account.
  - `initCode`: The init code of the sender smart contract account.
  - `callData`: The data to be sent to the sender smart contract account during execution.
  - `callGas`: The gas limit for the execution of the callData.
  - `verificationGas`: The gas limit for verifying the signature and nonce of the userOperation.
  - `preVerificationGas`: The gas limit for any operations before verifying the signature and nonce of the userOperation.
  - `maxFeePerGas`: The maximum fee per gas unit that can be paid by this userOperation.
  - `maxPriorityFeePerGas`: The maximum priority fee per gas unit that can be paid by this userOperation.
  - `paymasterAndData`: The address of the paymaster smart contract account that will sponsor this userOperation as well as any additional data required by the paymaster smart contract. This must be left blank, as this is what the wallet operator will have to fill out with the result of this call for the userOperation to be sponsored.
  - `signature`: The signature of this userOperation by its signer.
- `entryPoint`: The EntryPoint contract address the userOperation is being submitted to.
- `chainId`: The chainId of the chain this User Operation is being submitted on.
- `referralAddress`: A 20-byte hex address, likely owned by the wallet operator, that will accrue any referral fees from sponsored User Operations.

### Returns

- A JSON-RPC response object with a single member:
  - `paymasterAndData`: A hex string that represents an array of bytes. It contains information about whether this userOperation can be sponsored by
the Paymaster service and any additional data required by
the Paymaster service. If this userOperation cannot be sponsored, it returns an empty string.

### Example

Request:

```json
{
    "jsonrpc": "2.0",
    "method": "pm_sponsorUserOperation",
    "params": [
        {
            "sender": "0x1234567890123456789012345678901234567890",
            "nonce": "0x1",
            "initCode": "",
            "callData": "",
            "callGas": "0x100000",
            "verificationGas": "0x20000",
            "preVerificationGas": "0x10000",
            "maxFeePerGas": "0x3b9aca00",
            "maxPriorityFeePerGas": "0x3b9aca00",
            "paymasterAndData": "",
            "signature": ""
        },
        {
          "entryPoint": "0x0987654321098765432109876543210987654321"
        },
        {
          "chainId": "0x01"
        },
        {
          "referralAddress": "0x2109876543210987654301098765432198765432"
        }
    ],
    "id": "1"
}
```

Response:

```json
{
    "jsonrpc": "2.0",
    "result": {
      "paymasterAndData": "0xbcd12340a2109876543210987654301098765432198765432"
    },
    "id": "1"
}
```