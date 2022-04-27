# Multi Signature Wallet for Cardano + Staking Capability
Multi Signature wallet (multisig wallet) means a wallet that is not owned by a single entity or a person.

When using this wallet, transactions must be approved by a group of people that are responsible for this wallet.

The use-case for such a wallet is for an organization or a team who wants to create a *'Treasury'* that will hold their ADA.

## General overview
1. Instead of using one personal Wallet Address, we will use ‘Script Address’ to hold the funds
2. A script address is just like any other Cardano wallet address, where you can hold ADA, and send ADA from / to the address. The difference is, this wallet is not owned by a single ‘private key’.
3. This script address will have a pre-defined rules to only spend its UTXO if a certain conditions are met. This will defined in a script policy (a JSON structured file)
4. For this example, we will set a condition that **the script can only send ADA if a certain number of people specified in the script approve the transaction**
5. We will also create a script address that could also be staked, and withdraw the rewards together


## How it works
1. Create the script policy and the script address:
   1. `multisig-payment.policy` --> rules for doing regular transaction (payment key)
   2. `multisig-stake.policy` --> rules for withdrawing staking rewards (staking key)
   3. Creating the script address would be combining `multisig-payment.policy` and `multisig-stake.policy` together and then produce `multisig-payment-and-stake.addr`
2. This script will contain following information:
   1. List of wallet that are allowed to sign the transaction
   2. Minimum number of wallet required to validate transaction
   3. i.e: from 5 wallets listed, it will only requires 3 wallet to sign a transaction
3. Send ADA to this script address as treasury
4. To use the fund from this script address:
   1. One person would create a `Tx.raw` file that will consume `UTxO` from this script address – this is a transaction file that haven’t been signed by anyone, therefore it cannot be submitted into the blockchain
   2. The raw transaction would then be sent to each participants, and each of them will “sign” the `Tx.raw` file, and it will output a `Tx-person-1.witness` file
   3. Collecting `*.witness` files from the participants, one person would **“combine and build”** the `*.witness` files, and sign the `Tx.raw` to become `Tx.signed`
   4. Submit the signed transaction into the blockchain

## Detailed Steps
TBD
