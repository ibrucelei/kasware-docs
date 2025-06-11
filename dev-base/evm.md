# Getting Started with EVM networks

In order to provide support for Kaspa-based layer2 networks, the KasWare wallet has integrated support for EVM networks. When utilizing the KasWare wallet, users can directly submit layer2 transactions to Kaspa. Consequently, this offers protection against MEV attacks, which is a distinct advantage compared to other wallets.

EVM web apps can interact with KasWare wallet via the provider that is injected at window.kasware.ethereum. This provider conforms to the [EIP-1193](https://eips.ethereum.org/EIPS/eip-1193) standard and is also injected at window.ethereum to support legacy integrations. KasWare wallet also supports [EIP-6963](https://eip6963.org/) for ease of integration.

To detect if a user has already installed KasWare wallet, a web application should check for the existence of a kasware object.
If a kasware object exists, EVM dApps can interact with KasWare wallet via the API found at window.kasware.ethereum. This ethereum provider is also made available at window.ethereum but is prone to namespace collisions from other injected wallets.

To detect if KasWare wallet is installed, an application should check for an additional isKasWare flag.

```
const isKasWareInstalled= window?.kasware?.ethereum?.isKasWare;
```

If KasWare wallet is not installed, we recommend you redirect your users to our kasware officail website[https://www.kasware.xyz]({https://www.kasware.xyz}) to download the wallet. 