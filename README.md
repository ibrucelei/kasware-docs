# KasWare Wallet
Welcome to KasWare's Developer Documentation. This documentation is for learning to develop applications for KasWare Wallet.
## Getting Started
To develop for KasWare Wallet, install KasWare Wallet on your development machine.

Once KasWare Wallet is installed and running, you should find that new browser tabs have a window.kasware object available in the developer console. This is how your website will interact with KasWare Wallet.
### Browser Detection
To verify if the browser is running KasWare Wallet, copy and paste the code snippet below in the developer console of your web browser:
```javascript
if (typeof window.kasware !== 'undefined') {
  console.log('KasWare Wallet is installed!');
}
```
You can review the full API for the window.kasware object here.
### Connecting to KasWare Wallet
"Connecting" or "logging in" to KasWare Wallet effectively means "to access the user's Bitcoin account(s)".

You should **only** initiate a connection request in response to direct user action, such as clicking a button. You should **always** disable the "connect" button while the connection request is pending. You should **never** initiate a connection request on page load.

We recommend that you provide a button to allow the user to connect KasWare Wallet to your dapp. Clicking this button should call the following method:
```javascript
kasware.requestAccounts()
```
### Demo
​​
## Methods
### requestAccounts
```javascript
kasware.requestAccounts()
```
Connect the current account.
#### Parameters
none
#### Returns
- Promise returns string[] : Address of current account.
#### Example
```javascript
try {
  let accounts = await window.kasware.requestAccounts();
  console.log('connect success', accounts);
} catch (e) {
  console.log('connect failed');
}
> connect success ['tb1qrn7tvhdf6wnh790384ahj56u0xaa0kqgautnnz']
```
### getAccounts
```javascript
kasware.getAccounts()
```
Get address of current account
#### Parameters
none
#### Returns
- Promise - string: address of current account
#### Example
```javascript
try {
  let res = await window.kasware.getAccounts();
  console.log(res)
} catch (e) {
  console.log(e);
}
> ["tb1qrn7tvhdf6wnh790384ahj56u0xaa0kqgautnnz"]
```
### getNetwork
```javascript
kasware.getNetwork()
```
get network
#### Parameters
none
#### Returns
- Promise - string: the network. livenet and testnet
#### Example
```javascript
try {
  let res = await window.kasware.getNetwork();
  console.log(res)
} catch (e) {
  console.log(e);
}
​
> 0
```
### switchNetwork
```javascript
kasware.switchNetwork(network)
```
switch network
#### Parameters
- network - string: the network. livenet and testnet
#### Returns
none
#### Example
```javascript
try {
  let res = await window.kasware.switchNetwork("livenet");
  console.log(res)
} catch (e) {
  console.log(e);
}
​
> 0
```
### getPublicKey
```javascript
kasware.getPublicKey()
```
Get publicKey of current account.
#### Parameters
none
#### Returns
- Promise - string: publicKey
#### Example
```javascript
try {
  let res = await window.kasware.getPublicKey();
  console.log(res)
} catch (e) {
  console.log(e);
}
> 03cbaedc26f03fd3ba02fc936f338e980c9e2172c5e23128877ed46827e935296f
```
### getBalance
```javascript
kasware.getBalance()
```
Get BTC balance
#### Parameters
none
#### Returns
- Promise - Object:
  - confirmed - number : the confirmed satoshis
  - unconfirmed - number : the unconfirmed satoshis
  - total - number : the total satoshis
#### Example
```javascript
try {
  let res = await window.kasware.getBalance();
  console.log(res)
} catch (e) {
  console.log(e);
}
​
> {
    "confirmed":0,
    "unconfirmed":100000,
    "total":100000
  }
```
### sendBitcoin
```javascript
kasware.sendBitcoin(toAddress, satoshis, options)
```
Send BTC
#### Parameters
- toAddress - string: the address to send
- satoshis - number: the satoshis to send
- options - object:  (optional)
  - feeRate - number: the network fee rate
#### Returns
- Promise - string: txid
#### Example
```javascript
try {
  let txid = await window.kasware.sendBitcoin("tb1qrn7tvhdf6wnh790384ahj56u0xaa0kqgautnnz",1000);
  console.log(txid)
} catch (e) {
  console.log(e);
}
```
### signMessage
```javascript
kasware.signMessage(msg[, type])
```
sign message
#### Parameters
- msg - string: a string to sign
- type - string:  (Optional) "ecdsa" | "bip322-simple". default is "ecdsa"
#### Returns
- Promise - string: the signature.
#### Example
```javascript
// sign by ecdsa
try {
  let res = await window.kasware.signMessage("abcdefghijk123456789");
  console.log(res)
} catch (e) {
  console.log(e);
}
​
> G+LrYa7T5dUMDgQduAErw+i6ebK4GqTXYVWIDM+snYk7Yc6LdPitmaqM6j+iJOeID1CsMXOJFpVopvPiHBdulkE=
​
// verify by ecdsa
import { verifyMessage } from "@kasware/wallet-utils";
const pubkey = "026887958bcc4cb6f8c04ea49260f0d10e312c41baf485252953b14724db552aac";
const message = "abcdefghijk123456789";
const signature = "G+LrYa7T5dUMDgQduAErw+i6ebK4GqTXYVWIDM+snYk7Yc6LdPitmaqM6j+iJOeID1CsMXOJFpVopvPiHBdulkE=";
const result = verifyMessage(pubkey,message,signature);
console.log(result);
​
> true
​
// sign by bip322-simple
try {
  let res = await window.kasware.signMessage("abcdefghijk123456789","bip322-simple");
  console.log(res)
} catch (e) {
  console.log(e);
}
​
> AkcwRAIgeHUcjr0jODaR7GMM8cenWnIj0MYdGmmrpGyMoryNSkgCICzVXWrLIKKp5cFtaCTErY7FGNXTFe6kuEofl4G+Vi5wASECaIeVi8xMtvjATqSSYPDRDjEsQbr0hSUpU7FHJNtVKqw=
```

### pushTx

```javascript
kasware.pushTx(options)
```
Push Transaction
#### Parameters
- options - Object:
- rawtx - string: rawtx to push
#### Returns
- Promise - string: txid
#### Example
```javascript
try {
  let txid = await window.kasware.pushTx({
    rawtx:"0200000000010135bd7d..."
  });
  console.log(txid)
} catch (e) {
  console.log(e);
}
```
## Events
### accountsChanged
```javascript
kasware.on('accountsChanged', handler: (accounts: Array<string>) => void);
kasware.removeListener('accountsChanged', handler: (accounts: Array<string>) => void);
```
The accountsChanged will be emitted whenever the user's exposed account address changes.
### networkChanged
```javascript
kasware.on('networkChanged', handler: (network: string) => void);
kasware.removeListener('networkChanged', handler: (network: string) => void);
```
The networkChanged will be emitted whenever the user's network changes.