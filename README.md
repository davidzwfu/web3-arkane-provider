Venly Web3 Provider<img align="right" src="https://github.com/ArkaneNetwork.png?size=30" />
===
## Introduction

> The Venly Web3 provider is a smart wrapper around the existing Web3 Ethereum JavaScript API.

If you already have an application running using web3 technology, you can make use of this wrapper to leverage the full potential of Venly Wallet API.
Your existing infrastructure is just one code block away from being **Venly Wallet Enabled**.

![Venly Components](https://i.imgur.com/T5sWhZa.png)

## Documentation
The full documentation of the Venly Web3 Provider can be found here: https://docs.venly.io/widget/web3-provider/getting-started

## Installation

### NPM

Install and import the module in your project

```bash
npm i @venly/web3-provider
```

```javascript
import { VenlySubProvider } from "@venly/web3-provider";
```
### Browser

Alternatively, you can load the script from one of the following CDNs

```html
<script src="https://unpkg.com/@venly/web3-provider/umd/index.js"></script>
```

```html
<script src="https://cdn.jsdelivr.net/npm/@venly/web3-provider/umd/index.js"></script>
```

## Typing

To have types properly defined while using the library you need to place the code below inside the file you are intending to use the library.

```javascript
import { VenlySubProvider } from "@venly/web3-provider";

declare const Venly: VenlySubProvider;
```

## Using the Library

After adding the javascript file to your page, a global *Venly* object is added to your window. This object is the gateway for creating the web3 wrapper and fully integrates [Venly Connect](https://docs.venly.io/widget/widget/introduction).

### Adding the web3 provider

```javascript
const options: VenlyProviderOptions = {
  clientId: 'YOUR_CLIENT_ID',
  environment: 'staging', //optional, production by default  
  secretType: SecretType.ETHEREUM, //optional, ETHEREUM by default  
  windowMode: WindowMode.POPUP, //optional, POPUP by default
  bearerTokenProvider: () => 'obtained_bearer_token', //optional, default undefined
  skipAuthentication: false
};

Venly.createProviderEngine(options)
     .then(provider => {
         web3 = new Web3(provider);
     });
```

The web3 instance now works as if it was [injected by parity or metamask](https://github.com/ethereum/wiki/wiki/JavaScript-API). You can fetch your wallets or sign transactions and messages. 

If you provide your own implementation of `bearerTokenProvider`, the web3 provider will not attempt to obtain an authentication code, but rather use the one provided by you.

### Usage with ethers.js

Use the Web3Provider class to wrap our existing Web3-compatible provider and expose it as an ethers.js Provider. (requires ethers.js v5)

```javascript
ethers = new ethers.providers.Web3Provider(provider);
```

### Using Venly Connect natively

Although we use Venly Connect under the hood, the functionality of the web3 wrapper isn't limited to the web3 API. Linking or fetching profile information is not supported by Web3, but it is in our wrapper.
After creating a Venly Provider Engine, we add an instance of **VenlyConnect** to the global **Venly** object. As a result, it's possible to call Venly Connect natively, like so.

```
Venly.connect().linkWallets();
```

The full documentation of Venly Connect can be found here: https://docs.venly.io/widget/widget/introduction

# Example Project
We've created two examples of the Web3 Provider in our demo application.

One only checks authentication and shows the login form after the user clicks a button:
* [Web3 Provider Demo](https://demo.arkane.network/pages/web3-provider)
* [Web3 Provider Demo html source](https://github.com/ArkaneNetwork/Arketype/blob/develop/pages/web3-provider.html)
* [Web3 Provider JS source](https://github.com/ArkaneNetwork/Arketype/blob/develop/assets/js/web3-provider.js)

The other checks if a user is logged in on page load. If not, it shows the login button, otherwise it fetches the users' wallets:
* [Web3 Provider (skip auth) Demo](https://demo.arkane.network/pages/web3-provider-skip-auth)
* [Web3 Provider (skip auth) Demo html source](https://github.com/ArkaneNetwork/Arketype/blob/develop/pages/web3-provider-skip-auth.html)
* [Web3 Provider (skip auth) JS source](https://github.com/ArkaneNetwork/Arketype/blob/develop/assets/js/web3-provider-skip-auth.js)

# What is Venly Wallet
Not sure yet what Venly is all about, be sure to check out our website: https://www.venly.io/

## v2 Migration Guide

### Installation (changes only for head scripts)

```javascript
<script src="/node_modules/@venly/connect/umd/index.js"></script>
```

or when importing from a CDN

```javascript
<script src="https://unpkg.com/@venly/connect/umd/index.js"></script>
```

### Imports

All types/objects are now imported directly from `@venly/connect`

```javascript
import { Wallet } from "@venly/connect";
```

## Options

```typescript
type VenlyProviderOptions = {
  clientId: string
  environment: string
}
```

`clientId` - The Client ID is used to connect with Venly. See [here](https://docs.venly.io/widget/deep-dive/authentication#client-id) for more information.

`environment` - The environment to which you want to connect, possible values are 'staging' and 'production'. Default set to 'production'.
