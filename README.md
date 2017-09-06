# ethereum_hello_world
A simple ethereum contract for getting and transferring tokens.

### Requirements

- [testrpc](https://github.com/ethereumjs/testrpc)
- [truffle](https//github.com/trufflesuite/truffle)

To install these dependencies run `npm install -g ethereumjs-testrpc` and `npm install -g truffle`.

### Testing

1. clone the repo
3. `cd` into the directory
2. run `testrpc` in your terminal
3. compile the contract with `truffle compile`
4. run a migration using `truffle migrate`

Now you should be ready to play with the contract. Whenever you make changes to your code, you will need to recompile and run another migration for the changes to be available.

### Usage

run `truffle console` to load up a development network. By default you are the `owner` of the account.
1. Check the accounts.
  * you can check the accounts with `web3.eth.accounts`. This will return an array of hashes:
```[ '0xbfa103f847cb562a45e64dbc82618f72dfd2d51a',
  '0x5f25a8a03a943e024c8a8b848378d771900c9a36',
  '0xab217228e5ebe8e1b559f05f674a05faed804134',
  '0x9509c970e671e24b48f6c04af614e03dcf92c5f7',
  '0x47c905b95e588f0da2195f739a7d24289f3a6b7a',
  '0x454fb6144a146304ec96395aef637fddb7d4c033',
  '0x4e9ce86b157cb4955f8e3c772aeab47651073a98',
  '0x649dd383bfefff247775a36e9dc348b9f3f74094',
  '0x2f548708822721854695cc1098b8a0b0dd6715ad',
  '0x9e1f658143aca5cfd7335e2b263300914a6c7e24' ]
  ```
  
  2. Check the balance of the account
  
    * `HelloWorld.deployed().then(a => (a.getBalance(web3.eth.accounts[0]).then(console.log)))`. This will return the balance in an object like this:
  ``` [String: '1000'] s: 1, e: 3, c: [ 1000 ] } ```
  by default, the 0th user has an account balance of `1000`
  you can check other balances by passing in different indices to the `web3.eth.accounts[x]` for example, `HelloWorld.deployed().then(a => (a.getBalance(web3.eth.accounts[1]).then(console.log)))` gives us 
  ```{ [String: '0'] s: 1, e: 0, c: [ 0 ] }``` for a balance of 0.
  
  3. Transfer funds
  
    * you can transfer funds from your account to another with the `transfer()` function which take a `address` and a number as parameters. The address is the account you wish to transfer `TO` and the number is the amount you wish to transfer.
    * running ```HelloWorld.deployed().then(a => (a.transfer(web3.eth.accounts[1],25).then(console.log)))``` will give you the following receipt.
```{ tx: '0x8107a34296791c31c1ec207e4b54a03f42aad6b993272a842c2e2426462eeda1',
    receipt:
     { transactionHash: '0x8107a34296791c31c1ec207e4b54a03f42aad6b993272a842c2e2426462eeda1',
       transactionIndex: 0,
       blockHash: '0x62b487b61c6521822eafb605efb376ced7c75251ee06ee029b3310db0a8accfd',
       blockNumber: 5,
       gasUsed: 49166,
       cumulativeGasUsed: 49166,
       contractAddress: null,
       logs: [] },
    logs: [] }
  ```
    Checking the participating accounts will show the updated balances (+25 in account 1 and -25 in account 0)
