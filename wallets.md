# Wallets





## Get Coins
```json
curl "http://localhost:8657/api/coins"
-H "API-KEY: 359c26a316f97e17bf6b17169e6bd816"
-H "API-KEY-PASSPHRASE: Xwings2019"
-H "API-KEY-SECRET: x6NzNCWvCNSNnM/60QxKyRBqR/cl9gVQoDSv3ssn9ZM="
-X "GET"
```

> Sample response:

```json
{
    "coinResponses": [
        {
            "coin": "BTC",
            "decimals": 8
        },
        {
            "coin": "XRP",
            "decimals": 6
        },
        {
            "coin": "ETH",
            "decimals": 18
        },
        {
            "coin": "EOS",
            "decimals": 4
        },
        {
            "coin": "USDT",
            "decimals": 8
        }
    ]
}
```

Returns CoinObject.

### Supported Coins
DaGuard supports the following digital assets:

Id   	   | Digital Asset
-----------| --------------
BTC        | Bitcoin
USDT       | Tether
ETH        | Ether
EOS        | EOS
XRP        | Ripple

### HTTP Request
`GET /coins`
	
### CoinObject
Name               | Type(value)                     | Mandatory   | Description
-------------------| --------------------------------|-------------|-----------------------
coin               | String                          | M           | 
decimals           | Number                          | M           | 
contractAddress    | String                          | O           | 





## Get Coin
```json
curl "http://localhost:8657/api/coins/ETH"
-H "API-KEY: 359c26a316f97e17bf6b17169e6bd816"
-H "API-KEY-PASSPHRASE: Xwings2019"
-H "API-KEY-SECRET: x6NzNCWvCNSNnM/60QxKyRBqR/cl9gVQoDSv3ssn9ZM="
-X "GET"
```

> Sample response:

```json
{
    "coin": "ETH",
    "decimals": 18
}
```

Returns CoinObject.

### HTTP Request
`GET /coins/{coin}`




## Create Wallet
```json
curl "http://localhost:8657/api/wallets"
-H "API-KEY: 359c26a316f97e17bf6b17169e6bd816"
-H "API-KEY-PASSPHRASE: Xwings2019"
-H "API-KEY-SECRET: x6NzNCWvCNSNnM/60QxKyRBqR/cl9gVQoDSv3ssn9ZM="
-X "POST"
-H "Content-Type:application/json"
-d "{\"label\" : \"XRPACS\",\"coin\" : \"XRP\",\"walletPassphrase\" : \"Xwings2019\",\"backupPublicKey\":\"r4RTwsWi9MWMibc8HZ1gHYAt7jvz8SnUVm\"}"
```

> Sample response:

```json
{
  "walletId": "8ebc7ad9658d4941b2fdddcccf539371",
  "coin": "XRP",
  "label": "XRPACS",
  "userKey": "{\"version\":1,\"id\":\"49a2f4a828e771ccb4dee06a09b2c5d8\",\"crypto\":{\"cipher\":\"aes-128-ctr\",\"kdf\":\"scrypt\",\"ciphertext\":\"0R1jFXIa3mIGbWmPWn2ACDzjcqXz027hAN+jm5o=\",\"cipherparams\":{\"iv\":\"MqqjG7JTeVezty0YMDTYJA==\"},\"kdfparams\":{\"dklen\":32,\"n\":16384,\"p\":1,\"r\":8,\"salt\":\"RU1GiUr3PG0=\"}},\"pub\":\"rBZyi26m6MrmWfDECXBEW9pTaAKzVtdq7r\"}",
  "backupKey": "r4RTwsWi9MWMibc8HZ1gHYAt7jvz8SnUVm",
  "encryptedWalletPassword": "{\"cipher\":\"aes-128-ctr\",\"kdf\":\"scrypt\",\"ciphertext\":\"O4NoAOMcOFnISA==\",\"cipherparams\":{\"iv\":\"SHQreRcl/nLr9IKf1NyS9A==\"},\"kdfparams\":{\"dklen\":32,\"n\":16384,\"p\":1,\"r\":8,\"salt\":\"jh2wRWLZGso=\"}}"
}
```

Creates a coin Wallet object.


### HTTP Request
`POST /wallets`

### Body Parameters
Name                     | Type(value)       | Mandatory   | Description
-------------------------| ------------------|-------------|-----------------------
label                    | String            | M           | The label of this keycard
coin                     | String            | M           | The digital coin
walletPassphrase         | String            | M           | Encryption code for wallet passphrase (used for lost passphrase recovery)
backupPublicKey          | String            | O           | Backup Public Key


### Response
Name                       | Type(value)                 | Mandatory   | Description
---------------------------| ----------------------------|-------------|-----------------------
walletId                   | String                      | M           | Wallet id
label                      | String                      | M           | Wallet label
coin                       | String                      | M           | Coin id
userKey                    | String                      | M           | User Key, encrypted with provide passcode
backupKey                  | String                      | M           | Backup Key, encrypted with provide passcode
encryptedWalletPassword    | String                      | M           | wallet password, encrypted with a key held by Daguard
Those information which can be used to recover your wallet in several situations, please save it safely.




## Get Wallet
```json
curl "http://localhost:8657/api/BTC/wallets/38a67030909143da94a25f76ad3ac60c"
-H "API-KEY: 359c26a316f97e17bf6b17169e6bd816"
-H "API-KEY-PASSPHRASE: Xwings2019"
-H "API-KEY-SECRET: x6NzNCWvCNSNnM/60QxKyRBqR/cl9gVQoDSv3ssn9ZM="
-X "GET"
```

> Sample response:

```json
{
  "walletId": "38a67030909143da94a25f76ad3ac60c",
  "coin": "BTC",
  "label": "BTC_W1",
  "balance": "0",
  "availableBalance": "0",
  "keys": [
    "805d50bd5ffb13a5104deb68a8dd7166",
    "7ed3add5b0169bd82d8fac60b951f6eb",
    "25546cfe200cd7a956d3b484002054e0"
  ]
}
```

Returns a wallet object.

### HTTP Request
`GET /:coin/wallets/:walletId`

### Response
Name                 | Type(value)                 | Mandatory   | Description
---------------------| ----------------------------|-------------|-----------------------
walletId             | String                      | M           | Wallet id
label                | String                      | M           | Wallet label
coin                 | String                      | M           | Coin id
balance              | DoubleString                | M           | Wallet balance on blockchain
availableBalance     | DoubleString                | M           | Available balance for spending
keys                 | Array of String             | M           | Array of keyIds





## Get All Wallets
```json
curl "http://localhost:8657/api/BTC/wallets"
-H "API-KEY: 359c26a316f97e17bf6b17169e6bd816"
-H "API-KEY-PASSPHRASE: Xwings2019"
-H "API-KEY-SECRET: x6NzNCWvCNSNnM/60QxKyRBqR/cl9gVQoDSv3ssn9ZM="
-X "GET"
```

> Sample response:

```json
{
  "wallets": [
    {
      "walletId": "38a67030909143da94a25f76ad3ac60c",
      "coin": "BTC",
      "label": "BTC_W1",
      "balance": "0",
      "availableBalance": "0",
      "keys": [
        "805d50bd5ffb13a5104deb68a8dd7166",
        "7ed3add5b0169bd82d8fac60b951f6eb",
        "25546cfe200cd7a956d3b484002054e0"
      ]
    },
    {
      "walletId": "1e7101e060b740c793570b071562f99f",
      "coin": "BTC",
      "label": "BTC_W2",
      "balance": "0",
      "availableBalance": "0",
      "keys": [
        "89ad89e4ccf267e719014b9b7d075eff",
        "aa0479974a3fae3bf767870eb2b6e6b9",
        "be41f020ca5f28f7da929d6544f444e7"
      ]
    }
  ]
}
```

Returns an array of Wallet objects.

### HTTP Request
`GET /:coin/wallets`

### Response
Returns an array of Wallet objects. See [Get Wallet](#get-wallet) for the wallet object.










## Create Wallet Address
```json
curl "http://localhost:8657/api/BTC/wallets/b2993a9eb932437a9b742fa9f5267086/addresses"
-H "API-KEY: 359c26a316f97e17bf6b17169e6bd816"
-H "API-KEY-PASSPHRASE: Xwings2019"
-H "API-KEY-SECRET: x6NzNCWvCNSNnM/60QxKyRBqR/cl9gVQoDSv3ssn9ZM="
-X "POST"
-H "Content-Type:application/json"
-d '{"label":"address2"}'
```

> Sample response:

```json
{
  "address": "2NFstjMfj5EhDBUaKSFhjLZJ4PazqUZzqZ4",
  "coin": "BTC",
  "createdTime": 1546853432345635
}
```

### HTTP Request
`POST /:coin/wallets/:walletId/addresses`

### Body Parameters
Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
label            | String                          | M           | The label of this Address

### Response
Returns the created Address object. See [Get Wallet Address](#get-wallet-address) for the wallet address object.





## Get Wallet Address
```json
curl "http://localhost:8657/api/BTC/wallets/b2993a9eb932437a9b742fa9f5267086/addresses/2NFstjMfj5EhDBUaKSFhjLZJ4PazqUZzqZ4"
-H "API-KEY: 359c26a316f97e17bf6b17169e6bd816"
-H "API-KEY-PASSPHRASE: Xwings2019"
-H "API-KEY-SECRET: x6NzNCWvCNSNnM/60QxKyRBqR/cl9gVQoDSv3ssn9ZM="
-X "GET"
```

> Sample response:

```json
{
  "label": "Address 0",
  "address": "2NFstjMfj5EhDBUaKSFhjLZJ4PazqUZzqZ4",
  "coin": "BTC",
  "walletId": "b2993a9eb932437a9b742fa9f5267086",
  "createdTime": 1546833591910640
}
```

Returns Address object.

### HTTP Request
`GET /:coin/wallets/:walletId/addresses/:address`

### Response
Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
label            | String                          | M           | Address label
address          | String                          | M           | Coin address
coin             | String                          | M           | Coin id
walletId         | String                          | M           | Wallet id
createdTime      | Long                            | M           | Time the address was created





## Get Wallet All Addresses
```json
curl "http://localhost:8657/api/BTC/wallets/b2993a9eb932437a9b742fa9f5267086/addresses"
-H "API-KEY: 359c26a316f97e17bf6b17169e6bd816"
-H "API-KEY-PASSPHRASE: Xwings2019"
-H "API-KEY-SECRET: x6NzNCWvCNSNnM/60QxKyRBqR/cl9gVQoDSv3ssn9ZM="
-X "GET"
```

> Sample response:

```json
{
  "addresses": [
    {
      "label": "Address 0",
      "address": "2N7RYJawMLhhJ79q2ERTrb75MhGgofWXfQx",
      "coin": "BTC",
      "walletId": "b2993a9eb932437a9b742fa9f5267086",
      "createdTime": 1546833591910640
    },
    {
      "label": "address1",
      "address": "2NBwC2aLtXDAnHiEq7wSKfqGSGThdXhJwfu",
      "coin": "BTC",
      "walletId": "b2993a9eb932437a9b742fa9f5267086",
      "createdTime": 1546852394339506
    }
  ]
}
```

### HTTP Request
`GET /:coin/wallets/:walletId/addresses`
    
### Response
Returns an array of Address object. See [Get Wallet Address](#get-wallet-address) for the wallet address object.






## Get KeyChain
```json
curl "http://localhost:8657/api/BTC/key/4c5686cd551d95402db79fa62c83dd74"
-H "API-KEY: 359c26a316f97e17bf6b17169e6bd816"
-H "API-KEY-PASSPHRASE: Xwings2019"
-H "API-KEY-SECRET: x6NzNCWvCNSNnM/60QxKyRBqR/cl9gVQoDSv3ssn9ZM="
-X "GET"
```

> Sample response:

```json
{
    "id": "4c5686cd551d95402db79fa62c83dd74",
    "publicKey": "032ea9531ec1c024bcb8e3cc9f7f510e72f9ce029d8ab1922d262fd0f5feee76e7",
    "encryptedPrivateKey": "{\"cipher\":\"aes-128-ctr\",\"kdf\":\"scrypt\",\"ciphertext\":\"uypSM7i3bTsoTRZlIK61yu+zRYct4auQ/IJRpJityFkq60kUszqEwuVnG4vyVXpSUFCdAusx3c7Ro4ycg3KaKhkBXCyshvzvNJHMt7LNb8ZBoT1/CENCrLEtes5paCMH3HgZTU2VWzOCFLmiU9jn\",\"cipherparams\":{\"iv\":\"XjUGk075jo1c5K9RRge7Tw==\"},\"kdfparams\":{\"dklen\":32,\"n\":16384,\"p\":1,\"r\":8,\"salt\":\"K5qZ/GjFX7E=\"}}"
}
```

Returns KeyChainObject.

### HTTP Request
`GET /:coin/key/:keyId`
	
### KeyChainObject
Name               | Type(value)                     | Mandatory   | Description
-------------------| --------------------------------|-------------|-----------------------
id                 | String                          | M           | Key Id
publicKey          | String                          | M           | Public Key
encryptedPrivateKey| String                          | M           | Encrypted Private Key
