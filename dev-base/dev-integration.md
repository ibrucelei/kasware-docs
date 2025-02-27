# Integration with KasWare Wallet

Welcome to KasWare's integration documentation. This documentation is for learning to integrate KasWare wallet with your applications.
**Please note** : The integration API may be modified if relevant standards are officially released by kaspa core team one day in the future.

## Getting Started

First of all, install KasWare Wallet on your development machine. Once KasWare Wallet is installed and running, you should find that new browser tabs have a window.kasware object available in the developer console. This is how your website will interact with KasWare Wallet.

### Browser Detection

To verify if the browser is running KasWare Wallet, copy and paste the code snippet below in the developer console of your web browser:

```javascript
if (typeof window.kasware !== 'undefined') {
  console.log('KasWare Wallet is installed!');
}
```

You can review the full API for the window.kasware object here.

### Connecting to KasWare Wallet

"Connecting" or "logging in" to KasWare Wallet effectively means "to access the user's Kaspa account(s)".

You should **only** initiate a connection request in response to direct user action, such as clicking a button. You should **always** disable the "connect" button while the connection request is pending. You should **never** initiate a connection request on page load.

We recommend that you provide a button to allow the user to connect KasWare Wallet to your dapp. Clicking this button should call the following method:

```javascript
kasware.requestAccounts();
```

### Demo

<u>[Demo source code](https://github.com/kasware-wallet/dapp-demo)</u>
​​

## Methods

### requestAccounts

```javascript
kasware.requestAccounts();
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
> connect success ['kaspa:qzhkxxaully72gk23lyn7z3d9tdzdpw48ujsavrwlulekyk7pkxzzxj26hcsq']
```

### getAccounts

```javascript
kasware.getAccounts();
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
> ["kaspa:qzhkxxaully72gk23lyn7z3d9tdzdpw48ujsavrwlulekyk7pkxzzxj26hcsq"]
```

### getVersion

```javascript
kasware.getVersion();
```

get wallet version

#### Parameters

none

#### Returns

- Promise - string: wallet version

#### Example

```javascript
try {
  let res = await window.kasware.getVersion();
  console.log(res)
} catch (e) {
  console.log(e);
}
​
> '0.7.5.4'
```

### getNetwork

```javascript
kasware.getNetwork();
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
kasware.switchNetwork(network);
```

switch network

#### Parameters

- network - string: the network. mainnet/testnet/devnet

#### Returns

none

#### Example

```javascript
try {
  let res = await window.kasware.switchNetwork("mainnet");
  console.log(res)
} catch (e) {
  console.log(e);
}
​
> 0
```

### disconnect

```javascript
kasware.disconnect(origin);
```

disconnect kasware wallet

#### Parameters

- origin - string: website origin url

#### Returns

none

#### Example

```javascript
try {
  let origin = window.location.origin;
  await kasware.disconnect(origin);
} catch (e) {
  console.log(e);
}
​
> 0
```

### getPublicKey

```javascript
kasware.getPublicKey();
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
kasware.getBalance();
```

Get KAS balance

#### Parameters

none

#### Returns

- Promise - Object:
  - confirmed - number : the confirmed sompi
  - unconfirmed - number : the unconfirmed sompi
  - total - number : the total sompi

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

### getKRC20Balance

```javascript
kasware.getKRC20Balance();
```

Get KRC20 token balance

#### Parameters

none

#### Returns

- Promise - Array of Object:
  - balance: string;
  - dec: string;
  - locked: string;
  - opScoreMod: string;
  - tick: string;

#### Example

```javascript
try {
  let res = await window.kasware.getKRC20Balance();
  console.log(res)
} catch (e) {
  console.log(e);
}
​
> {
    balance: "287999890000000"
    dec: "8"
    locked: "0"
    opScoreMod: "905940300025"
    tick: "XXXX"
  }
```

### sendKaspa

```javascript
kasware.sendKaspa(toAddress, sompi, options);
```

Send KAS

#### Parameters

- toAddress - string: the address to send
- sompi - number: the sompi to send
- options - object: (optional)
  - priorityFee - number: the network prioity fee. default is 0. Unit is sompi
  - payload - string: payload for transactions

#### Returns

- Promise - string: txid

#### Example

```javascript
try {
  let txid = await window.kasware.sendKaspa(
    'kaspa:qzhkxxaully72gk23lyn7z3d9tdzdpw48ujsavrwlulekyk7pkxzzxj26hcsq',
    1000
  );
  console.log(txid);
} catch (e) {
  console.log(e);
}
```

### Demo Code For KRC20 Marketplace

<u>[Demo Code For KRC20 Marketplace](https://github.com/kasware-wallet/dapp-demo/blob/krc20_marketplace/src/App.tsx)</u>

### createKRC20Order

```javascript
kasware.createKRC20Order({krc20Tick, krc20Amount, kasAmount, psktExtraOutput, priorityFee});
```

Create a KRC20 Order to sell KRC20 token

#### Parameters

- krc20Tick - string: krc20 token tick
- krc20Amount - number || string: the amount of KRC20 token to sell, Unit is KRC20 token
- kasAmount - number: total selling price. Unit is kas
- psktExtraOutput - {address:string; amount: number }[]:(optional) use psktExtraOutput to create a service fee or other things
- priorityFee - number:(optional) the network prioity fee. default is 0. Unit is kas.

#### Returns

- Promise - { txJsonString: string, sendCommitTxId:string }: txJsonString is the pskt json string, sendCommitTxId is the commit transaction id of Send OP

#### Example:

```javascript
try {
      const krc20Tick = "aaaa";
      const krc20Amount = 10;
      const kasAmount = 490;
      const psktExtraOutput = [
        { address: "kaspatest:qrpygfgeq45h68wz5pk4rtay02w7fwlhax09x4rsqceqq6s3mz6uctlh3a695", amount: 0.2 },
      ];
      const priorityFee = 0;
      const { txJsonString, sendCommitTxId } = await (window as any).kasware.createKRC20Order({
        krc20Tick,
        krc20Amount,
        kasAmount,
        psktExtraOutput,
        priorityFee,
      });

} catch (e) {
  console.log(e);
}
```


### buyKRC20Token

<u>[Demo Code For buyKRC20Token()](https://github.com/kasware-wallet/dapp-demo/blob/1c3d992168e434e9d61c704afe1b992ff421625c/src/App.tsx#L619)</u>

```javascript
kasware.buyKRC20Token({txJsonString, extraOutput, priorityFee});
```

#### Parameters

- txJsonString - string: a pskt json string from the createKRC20Order() function
- extraOutput - {address:string; amount: number }[]: (optional) use extraOutput to create a service fee or other things
- priorityFee - number: (optional) the network prioity fee. default is 0. Unit is kas.

#### Returns

- Promise - txId: transaction id


### cancelKRC20Order
<u>[Demo Code For cancelKRC20Order()](https://github.com/kasware-wallet/dapp-demo/blob/1c3d992168e434e9d61c704afe1b992ff421625c/src/App.tsx#L642C50-L642C66)</u>

```javascript
kasware.cancelKRC20Order({krc20Tick, txJsonString, sendCommitTxId });
```

#### Parameters

- krc20Tick - string: krc20 token tick
- txJsonString - string: (optional) a pskt json string from the createKRC20Order() function
- sendCommitTxId - string: (optional) sendCommitTxId is the commit transaction id of Send OP from the createKRC20Order() function



#### Returns

- Promise - txId: transaction id



### signMessage

```javascript
kasware.signMessage(msg[, type])
```

sign message

#### Parameters

- msg - string: a string to sign
- type - string: (Optional) "ecdsa" | "bip322-simple". default is "ecdsa"

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

const pubkey = "026887958bcc4cb6f8c04ea49260f0d10e312c41baf485252953b14724db552aac";
const message = "abcdefghijk123456789";
const signature = "G+LrYa7T5dUMDgQduAErw+i6ebK4GqTXYVWIDM+snYk7Yc6LdPitmaqM6j+iJOeID1CsMXOJFpVopvPiHBdulkE=";
const result = kasware.verifyMessage(pubkey,message,signature);
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

### signKRC20Transaction

```javascript
kasware.signKRC20Transaction(inscribeJsonString, type, destAddr, priorityFee);
```

Sign KRC20 Transaction

#### Parameters

- inscribeJsonString - string: stringified json object
- type - number: 2 for deployment, 3 for mint, 4 for transfer
- destAddr - string:(optional) the address to transfer. it's an optional parameter. only used for transfer
- priorityFee - number:(optional) the network prioity fee. default is 0. Unit is kas.

#### Returns

- Promise - string: txid

#### Example-1: deploy a KRC20 token

```javascript
try {
  const deployJsonString =
    '{"p":"KRC-20","op":"deploy","tick":"BBBB","max":"21000000000000000000000000000000","lim":"100000000000000000000", "pre":"100000000000000000000"}';
  const type = 2;
  let txid = await window.kasware.signKRC20Transaction(
    inscribeJsonString,
    type
  );
  console.log(txid);
} catch (e) {
  console.log(e);
}
```

#### Example-2: mint a KRC20 token

```javascript
try {
  const inscribeJsonString = '{"p":"KRC-20","op":"mint","tick":"XXXX"}';
  const type = 3;
  let txid = await window.kasware.signKRC20Transaction(
    inscribeJsonString,
    type
  );
  console.log(txid);
} catch (e) {
  console.log(e);
}
```

#### Example-3: transfer a KRC20 token

```javascript
try {
  const transferJsonString =
    '{"p":"KRC-20","op":"transfer","tick":"RBMV","amt":"10000000000","to":"kaspa:qzhkxxaully72gk23lyn7z3d9tdzdpw48ujsavrwlulekyk7"}';
  const type = 4;
  const destAddr = 'kaspa:qzhkxxaully72gk23lyn7z3d9tdzdpw48ujsavrwlulekyk7';
  let txid = await window.kasware.signKRC20Transaction(
    inscribeJsonString,
    type,
    destAddr
  );
  console.log(txid);
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

### balanceChanged

```javascript
kasware.on('balanceChanged', handler: (balance: IBalance) => void);
kasware.removeListener('balanceChanged', handler: (balance: IBalance) => void);;
```

The balaneChanged will be emitted whenever the user's balance changes.
#### Example

```javascript
kasware.on('balanceChanged', (balance) => {
  console.log(balance);
  // example
    {
        address: "kaspa:qp2vyqkuanrqn38362wa5ja93e3se4cv3zqa8yhjalrj24n3g2t52hwx299ku",
        balance: {
            mature: 1699956916,
            pending: 199988333,
            outgoing: 0,
            matureUtxoCount: 1,
            pendingUtxoCount: 1,
            stasisUtxoCount: 0
        }
    }
});
```

### transactionReplacementResponse

```javascript
kasware.on('transactionReplacementResponse', handler: (response: { transactionId:string, replacedTransactionId:string }) => void);
kasware.removeListener('transactionReplacementResponse', handler: (response: transactionId:string, replacedTransactionId:string ) => void);;
```

The transactionReplacementResponse will be emitted whenever the user pushes a rbf transaction.
#### Example

```javascript
kasware.on('transactionReplacementResponse', (res) => {
  console.log(res);
  // example
    {
        transactionId: "c353c038d18a2455b72ea02ed47b4e34a60577435f6eba88f940c591c6405ca5",
        replacedTransactionId: "40a6fa1b3611bb4d34f9d8d91a90f46b3e0b6a5f1b0663de8bbe58bec2f3ecdg"
    }
});
```
