# Secret-SCRT - Privacy coin backed by SCRT

This is a quick and dirty PoC of how to create a privacy token on the Secret Network backed by a native coin.

Usage is pretty simple - you deposit SCRT into the contract, and you get SSCRT (or Secret-SCRT), which you can then use with the ERC-20-like functionality that the contract provides including: sending/receiving/allowance and withdrawing back to SCRT. 

In terms of privacy the deposit & withdrawals are public, as they are transactions on-chain. The rest of the functionality is private (so no one can see if you send SSCRT and to whom, and receiving SSCRT is also hidden). 

One caveat is that in order to achieve this level of privacy, querying your balance is done as a transaction (and so you must pay fees and wait for an on-chain response) rather than a free query. This is done to be able to validate the account sender and keep your balance hidden from others, otherwise anyone would be able to query anyone else's balance.

This is a slightly naive implementation, and more advanced uses could find creative ways to allow wallets to still notify you of incoming transactions without paying excessive fees, but that is an execise left to the reader.

The usual disclaimer: Don't use this in production, I take no responsibility for anything anywhere anytime etc.

## Usage examples:


To deposit: ***(This is public)***

```./secretcli tx compute <contract-address> '{"deposit": {}}' --sent-funds 1000000uscrt```

To send SSCRT: ***(Only you will be able to see the parameters you send here)***

```./secretcli tx compute <contract-address> '{"send": {"address": "<destination_address>"}}'```

To check your balance: ***(Only you will be able to see the parameters you send here)***

```./secretcli tx compute <contract-address> '{"balance": {}}'```
```./secretcli q compute tx <returned tx-hash>```
