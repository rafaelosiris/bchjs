# BchJS: Bitcoin Cash library blockchain interaction and different purpose for Node.js and web browsers.


Easy JavaScript library for Bitcoin Cash blockchain interaction needs. Easy-to-use, thoroughly tested and complete.

Support for the new Bitcoin Cash address ABC which improves upon [BIP 173](https://github.com/bitcoin/bips/blob/master/bip-0173.mediawiki), as well as the Bitpay and Legacy formats.

Test a demo address translator powered by BchAddr.js [here](https://bitcoincashjs.github.io/address/).

## Installation

### Web Browser Manually Script Tag

You may include a script tag in your HTML and the `bchaddr` module will be defined globally on subsequent scripts.

```html
<html>
  <head>
    ...
    <script src="https://github.com/rafaelosiris/bchjs/library/bchaddrjs-0.3.0.min.js"></script>
  </head>
  ...
</html>
```

## Code Examples

### Supported formats, networks and address types.
```javascript
var Format = bchaddr.Format; // Legacy, Bitpay or Cashaddr.
var Network = bchaddr.Network; // Mainnet or Testnet.
var Type = bchaddr.Type; // P2PKH or P2SH.
```

### Test for address format.
```javascript
var isLegacyAddress = bchaddr.isLegacyAddress;
var isBitpayAddress = bchaddr.isBitpayAddress;
var isCashAddress = bchaddr.isCashAddress;

isLegacyAddress('1B9UNtBfkkpgt8kVbwLN9ktE62QKnMbDzR') // true
isLegacyAddress('qph5kuz78czq00e3t85ugpgd7xmer5kr7c5f6jdpwk') // false
isBitpayAddress('CScMwvXjdooDnGevHgfHjGWFi9cjk75Aaj') // true
isBitpayAddress('1B9UNtBfkkpgt8kVbwLN9ktE62QKnMbDzR') // false
isCashAddress('qph5kuz78czq00e3t85ugpgd7xmer5kr7c5f6jdpwk') // true
isCashAddress('CScMwvXjdooDnGevHgfHjGWFi9cjk75Aaj') // false
```

### Test for address network.
```javascript
var isMainnetAddress = bchaddr.isMainnetAddress;
var isTestnetAddress = bchaddr.isTestnetAddress;

isMainnetAddress('1P238gziZdeS5Wj9nqLhQHSBK2Lz6zPSke') // true
isMainnetAddress('mnbGP2FeRsbgdQCzDT35zPWDcYSKm4wrcg') // false
isTestnetAddress('qqdcsl6c879esyxyacmz7g6vtzwjjwtznsggspc457') // true
isTestnetAddress('CeUvhjLnSgcxyedaUafcyo4Cw9ZPwGq9JJ') // false
```

### Test for address type.
```javascript
var isP2PKHAddress = bchaddr.isP2PKHAddress;
var isP2SHAddress = bchaddr.isP2SHAddress;

isP2PKHAddress('1Mdob5JY1yuwoj6y76Vf3AQpoqUH5Aft8z') // true
isP2PKHAddress('2NFGG7yRBizUANU48b4dASrnNftqsNwzSM1') // false
isP2SHAddress('H92i9XpREZiBscxGu6Vx3M8jNGBKqscBBB') // true
isP2SHAddress('CeUvhjLnSgcxyedaUafcyo4Cw9ZPwGq9JJ') // false
```

### Detect address format.
```javascript
var detectAddressFormat = bchaddr.detectAddressFormat;

detectAddressFormat('qqdcsl6c879esyxyacmz7g6vtzwjjwtznsggspc457') // Format.Cashaddr
detectAddressFormat('CScMwvXjdooDnGevHgfHjGWFi9cjk75Aaj') // Format.Bitpay
```

### Detect address network.
```javascript
var detectAddressNetwork = bchaddr.detectAddressNetwork;

detectAddressNetwork('1P238gziZdeS5Wj9nqLhQHSBK2Lz6zPSke') // Network.Mainnet
detectAddressNetwork('qqdcsl6c879esyxyacmz7g6vtzwjjwtznsggspc457') // Network.Testnet
```

### Detect address type.
```javascript
var detectAddressType = bchaddr.detectAddressType;

detectAddressType('1P238gziZdeS5Wj9nqLhQHSBK2Lz6zPSke') // Type.P2PKH
detectAddressType('3NKpWcnyZtEKttoQECAFTnmkxMkzgbT4WX') // Type.P2SH
```

### Translate address from any address format into a specific format.
```javascript
var toLegacyAddress = bchaddr.toLegacyAddress;
var toBitpayAddress = bchaddr.toBitpayAddress;
var toCashAddress = bchaddr.toCashAddress;

toLegacyAddress('qph5kuz78czq00e3t85ugpgd7xmer5kr7c5f6jdpwk') // 1B9UNtBfkkpgt8kVbwLN9ktE62QKnMbDzR
toBitpayAddress('1B9UNtBfkkpgt8kVbwLN9ktE62QKnMbDzR') // CScMwvXjdooDnGevHgfHjGWFi9cjk75Aaj
toCashAddress('1B9UNtBfkkpgt8kVbwLN9ktE62QKnMbDzR') // bitcoincash:qph5kuz78czq00e3t85ugpgd7xmer5kr7c5f6jdpwk
```

## Documentation and Help

rafaelosiris@gmail.com 

