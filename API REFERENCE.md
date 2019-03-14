# API General
All API requests and responses use application/json content type. Responses	follow HTTP response status codes to indicate
the success and the failure.



## API Base Url 
`http://localhost:8657/api`



## API Request

### API Request Headers
All API requests must contain the following headers:

* API-KEY
* API-KEY-SECRET
* API-KEY-PASSPHRASE



## API Response
Successful http response contains HTTP status code 200 and an optional body. If the response contains the body,
 the fields within the body are documented in each related API sections.  Failed http response contains non 200 HTTP status
code and the body with an errorCode field to indicate the cause of the failures.

### Error Response Fields
Name         | Type        | Mandatory | Description
------------ | ------------| ----------| -----------------------------------------------------------------------------------------
errorCode    | String      | M         | Error code. e.g.INVALID_PASSWORD
errorData    | String      | O         | Additional information on the user data that may cause the error. Data is provided in json format.



## API Message Format
All messages are in json format.

### API Message Field Types
Type         | Description
------------ | ------------
Integer      | Integer numbers
Long         | Long numbers
Boolean      | True/False
DoubleString | Decimal numbers are returned as strings to preserve full precision across platforms
Enum         | Enum definition. Passing invalid enum values will result in API_BAD_REQUEST error
String       | Text

### API Message Mandatory Field Indicators
Indicator    | Description
------------ | ----------------------------------------
M            | Mandatory field
(M)          | Mandatory field under certain conditions
O            | Optional field



## Pagination
Pagination is supported for all REST calls that return arrays. The newest items are returned by default.

Name	   | Type(value)| Mandatory| Description
-----------| -----------|----------|-------------------
pageNumber | Integer    | O        | Default to 1
pageSize   | Integer    | O	       | Default to 100

Example: GET transfers?pageNumber=1&pageSize=100



## Timestamp
Unless otherwise specified, all timestamps returned from API are milliseconds since UNIX Epoch.












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















# Transfers

## Create Transfer Request
```json
curl "http://localhost:8657/api/BTC/wallets/b2993a9eb932437a9b742fa9f5267086/transferRequests"
-H "API-KEY: 359c26a316f97e17bf6b17169e6bd816"
-H "API-KEY-PASSPHRASE: Xwings2019"
-H "API-KEY-SECRET: x6NzNCWvCNSNnM/60QxKyRBqR/cl9gVQoDSv3ssn9ZM="
-X "POST"
-H "Content-Type:application/json"
-d '{"amount":"0.00002","walletPassPhrase":"123456","toAddress":"2MsYKTgDCqy5HqrJxJFo3w9fpG63kGxRwFC"}'
```

> Sample response:

```json
{
  "transferRequestId": "4c9c8e67981244f7ad81d7f04402bf41",
  "coin": "BTC",
  "walletId": "773988afc53347e48aa9100ac0c24d48",
  "toAddress": "2MsYKTgDCqy5HqrJxJFo3w9fpG63kGxRwFC",
  "amount": "0.00002",
  "transferState": "APPROVED",
  "approvalsRequired": 0,
  "createdTime": 1546862366781588,
  "createdBy": "8f1d99de6db74f948e22603bced34386",
  "txData": "eyJoZXgiOiIwMTAwMDAwMDAxNzcwOWYwZmQyOWU3NmI3ZjlkMDJmZTBkNzZmNmE2Y2RkZTA2YWZmOWUyMjA5ZjNkZDE3YmVjY2Y1YjQzNDVkMTAxMDAwMDAwMDBmZmZmZmZmZjAyZDAwNzAwMDAwMDAwMDAwMDE3YTkxNDAzM2JhM2FmMDQ3MjQyYWRhZjM4ZmQ2NjYwYTRlMWZkMjE1ZGQ0OWU4N2I0MzYwMDAwMDAwMDAwMDAxN2E5MTQ4OWVhNmI5NmZiZGY3NDkzNzcwNGMyYTIxOTQ0ZWViOTIzNGJjZjE5ODcwMDAwMDAwMCIsInZpbiI6W3siYWRkcmVzcyI6IjJONXBUUE5UZG9mRXhuenpyZDZSNkNlTUJuZVpLV0V4SjRWIiwidHhpZCI6ImQxNDU0MzViY2ZlYzdiZDEzZDlmMjBlMmY5YWYwNmRlY2RhNmY2NzYwZGZlMDI5ZDdmNmJlNzI5ZmRmMDA5NzciLCJ2b3V0IjoxLCJhbW91bnQiOjE2NDQ4LCJyZWRlZW1TY3JpcHQiOiI1MjIxMDM1OGYzYTc0M2IwNTM5MDMzZGFkY2RmNTYxNDhiZGIxZTc4OTAxZmY0OTdkODRiMzE1NjI2MjRkNWZjNGU0YjYxMjEwMzZlM2EyZWU1ZmU1YWY5Y2MzMDExMzEyMDRmYTQ3YThkZTNjN2UyNjkzNjdlYWMxMTI0NmNmMjczNWIwZmNiNzQyMTAzZTU4ZTU2MWFjYzJjYTUyMWY0MGJmNzFjYTVjYzFmZDdiMWFhMzJkNmM3MTlkMjY4YzZmYTAwZWEwNTJhYjk3YjUzYWUiLCJ0YW5rIjpmYWxzZSwic2VxdWVuY2UiOjB9XSwidjEiOm51bGwsInIxIjpudWxsLCJzMSI6bnVsbCwidjIiOm51bGwsInIyIjpudWxsLCJzMiI6bnVsbCwiZnJvbUFkZHJlc3NlcyI6WyIyTjVwVFBOVGRvZkV4bnp6cmQ2UjZDZU1CbmVaS1dFeEo0ViJdLCJ0b0FkZHJlc3MiOiIyTXNZS1RnRENxeTVIcXJKeEpGbzN3OWZwRzYza0d4UndGQyIsImFtb3VudCI6IjAuMDAwMDIiLCJmZWUiOiIwLjAwMDAwNDQ0In0="
}
```

### HTTP Request
`POST /:coin/wallets/:walletId/transferRequests`

### Body Parameters
Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
walletPassphrase | String                          | M           | Wallet pass phrase
amount           | DoubleString                    | M           | The amount to be sent
toAddress        | String                          | M           | The address to send to
comment          | String                          | O           | Notes for the transfer

### Response
Returns the created transfer request object. See [Get Transfer Request](#get-transfer-request) for the transfer request object.





## Get Transfer Request
```json
curl "http://localhost:8657/api/BTC/wallets/b2993a9eb932437a9b742fa9f5267086/transferRequests/4c9c8e67981244f7ad81d7f04402bf41"
-H "API-KEY: 359c26a316f97e17bf6b17169e6bd816"
-H "API-KEY-PASSPHRASE: Xwings2019"
-H "API-KEY-SECRET: x6NzNCWvCNSNnM/60QxKyRBqR/cl9gVQoDSv3ssn9ZM="
-X "GET"
```

> Sample response:

```json
{
  "transferRequestId": "4c9c8e67981244f7ad81d7f04402bf41",
  "coin": "BTC",
  "walletId": "773988afc53347e48aa9100ac0c24d48",
  "toAddress": "2MsYKTgDCqy5HqrJxJFo3w9fpG63kGxRwFC",
  "amount": "0.00002",
  "transferState": "APPROVED",
  "approvalsRequired": 0,
  "createdTime": 1546862366781588,
  "createdBy": "8f1d99de6db74f948e22603bced34386",
  "txData": "eyJoZXgiOiIwMTAwMDAwMDAxNzcwOWYwZmQyOWU3NmI3ZjlkMDJmZTBkNzZmNmE2Y2RkZTA2YWZmOWUyMjA5ZjNkZDE3YmVjY2Y1YjQzNDVkMTAxMDAwMDAwMDBmZmZmZmZmZjAyZDAwNzAwMDAwMDAwMDAwMDE3YTkxNDAzM2JhM2FmMDQ3MjQyYWRhZjM4ZmQ2NjYwYTRlMWZkMjE1ZGQ0OWU4N2I0MzYwMDAwMDAwMDAwMDAxN2E5MTQ4OWVhNmI5NmZiZGY3NDkzNzcwNGMyYTIxOTQ0ZWViOTIzNGJjZjE5ODcwMDAwMDAwMCIsInZpbiI6W3siYWRkcmVzcyI6IjJONXBUUE5UZG9mRXhuenpyZDZSNkNlTUJuZVpLV0V4SjRWIiwidHhpZCI6ImQxNDU0MzViY2ZlYzdiZDEzZDlmMjBlMmY5YWYwNmRlY2RhNmY2NzYwZGZlMDI5ZDdmNmJlNzI5ZmRmMDA5NzciLCJ2b3V0IjoxLCJhbW91bnQiOjE2NDQ4LCJyZWRlZW1TY3JpcHQiOiI1MjIxMDM1OGYzYTc0M2IwNTM5MDMzZGFkY2RmNTYxNDhiZGIxZTc4OTAxZmY0OTdkODRiMzE1NjI2MjRkNWZjNGU0YjYxMjEwMzZlM2EyZWU1ZmU1YWY5Y2MzMDExMzEyMDRmYTQ3YThkZTNjN2UyNjkzNjdlYWMxMTI0NmNmMjczNWIwZmNiNzQyMTAzZTU4ZTU2MWFjYzJjYTUyMWY0MGJmNzFjYTVjYzFmZDdiMWFhMzJkNmM3MTlkMjY4YzZmYTAwZWEwNTJhYjk3YjUzYWUiLCJ0YW5rIjpmYWxzZSwic2VxdWVuY2UiOjB9XSwidjEiOm51bGwsInIxIjpudWxsLCJzMSI6bnVsbCwidjIiOm51bGwsInIyIjpudWxsLCJzMiI6bnVsbCwiZnJvbUFkZHJlc3NlcyI6WyIyTjVwVFBOVGRvZkV4bnp6cmQ2UjZDZU1CbmVaS1dFeEo0ViJdLCJ0b0FkZHJlc3MiOiIyTXNZS1RnRENxeTVIcXJKeEpGbzN3OWZwRzYza0d4UndGQyIsImFtb3VudCI6IjAuMDAwMDIiLCJmZWUiOiIwLjAwMDAwNDQ0In0="
}
```

Returns Transfer Request Object.

### HTTP Request
`GET /:coin/wallets/:walletId/transferRequests/:transferRequestId`

### Response
Name               | Type(value)                     | Mandatory   | Description
-------------------| --------------------------------|-------------|-----------------------
transferRequestId  | String                          | M           | Transfer request id
coin               | String                          | M           | Coin Id
walletId           | String                          | M           | Wallet Id
toAddress          | String                          | M           | Send to address
amount             | DoubleString                    | M           | The amount to be sent
comment            | String                          | O           | Notes for the transfer
transferState      | Enum                            | M           | Please refer to [transferState](#transfer-state) in enums
approvalsRequired  | Integer                         | M           | Number of approvals required
createdTime        | Long                            | M           | Created time
createdBy          | String                          | M           | User id that is used to create the transfer request
apiKey             | String                          | O           | Exists if the request is sent through api
transferId         | String                          | O           | Transfer id
txid               | String                          | O           | Txid on blockchain
txData             | String                          | M           | Unsigned transaction or half sign transaction data encoded by BASE64





## Get Pending Approval Transfer Requests
```json
curl "http://localhost:8657/api/BTC/wallets/773988afc53347e48aa9100ac0c24d48/transferRequests?transferState=PENDING_APPROVAL"
-H "API-KEY: 359c26a316f97e17bf6b17169e6bd816"
-H "API-KEY-PASSPHRASE: Xwings2019"
-H "API-KEY-SECRET: x6NzNCWvCNSNnM/60QxKyRBqR/cl9gVQoDSv3ssn9ZM="
-X "GET"
```

> Sample response:

```json
{
  "transferRequestResponses": [
    {
      "transferRequestId": "5b47858edce04ac2a81613c4d349cf37",
      "coin": "BTC",
      "walletId": "773988afc53347e48aa9100ac0c24d48",
      "toAddress": "2MsYKTgDCqy5HqrJxJFo3w9fpG63kGxRwFC",
      "amount": "0.0003",
      "transferState": "PENDING_APPROVAL",
      "approvalsRequired": 1,
      "createdTime": 1546927220768907,
      "createdBy": "8f1d99de6db74f948e22603bced34386",
      "txData": "eyJoZXgiOiIwMTAwMDAwMDAxMmViYTQ0N2RjM2Q1NWQ0MDM4MzBmNDQ5MDBmMmJjMWEzNTEzZmExNTU2ZGUxYmE4YjNmOWFlNGUxOGMxMTE1ZDAxMDAwMDAwYjQwMDQ3MzA0NDAyMjAyMzcxOTQ4NzM1YjQ1OWM5ZjkzYWE5ZWM4NWU5ZDBhMGVhZjE1MzRjNTYyMDA5ZDJiNTg0NDM1N2Y1OTdiNWI1MDIyMDM0NDU5YWI1ZjQ0ZjFlNmFkMzI0N2RlYjcwYzM4MjY1MmY1M2Q5NjRhZDZmYTAxZDk2OTc3NzMwN2FjMzM5ZjkwMTRjNjk1MjIxMDM1OGYzYTc0M2IwNTM5MDMzZGFkY2RmNTYxNDhiZGIxZTc4OTAxZmY0OTdkODRiMzE1NjI2MjRkNWZjNGU0YjYxMjEwMzQ3MDUzNmFmZGY0N2M0ZWQ2ODM2ZGU4MWZiYjFmZWRlZjBhMzA0NjJmZGNlYWJjMDU4YzE0MDMzYjAyNTkyYzkyMTAzZTU4ZTU2MWFjYzJjYTUyMWY0MGJmNzFjYTVjYzFmZDdiMWFhMzJkNmM3MTlkMjY4YzZmYTAwZWEwNTJhYjk3YjUzYWVmZmZmZmZmZjAyMzA3NTAwMDAwMDAwMDAwMDE3YTkxNDAzM2JhM2FmMDQ3MjQyYWRhZjM4ZmQ2NjYwYTRlMWZkMjE1ZGQ0OWU4N2EzZmVlMjAwMDAwMDAwMDAxN2E5MTQ2ODhhMjFiNTA0NGQwYzg3MDQzM2VmZTNmN2IwNzhkOWVhMTg2OGFlODcwMDAwMDAwMCIsInZpbiI6W3siYWRkcmVzcyI6IjJOMm15am5wb2RUV2VCOFZ0OUVaOEF3d2M3a1dLZDFWa01kIiwidHhpZCI6IjVkMTFjMTE4NGVhZWY5YjNhODFiZGU1NjE1ZmExMzM1MWFiY2YyMDA0OWY0MzAzODQwNWRkNWMzN2Q0NGJhMmUiLCJ2b3V0IjoxLCJyZWRlZW1TY3JpcHQiOiI1MjIxMDM1OGYzYTc0M2IwNTM5MDMzZGFkY2RmNTYxNDhiZGIxZTc4OTAxZmY0OTdkODRiMzE1NjI2MjRkNWZjNGU0YjYxMjEwMzQ3MDUzNmFmZGY0N2M0ZWQ2ODM2ZGU4MWZiYjFmZWRlZjBhMzA0NjJmZGNlYWJjMDU4YzE0MDMzYjAyNTkyYzkyMTAzZTU4ZTU2MWFjYzJjYTUyMWY0MGJmNzFjYTVjYzFmZDdiMWFhMzJkNmM3MTlkMjY4YzZmYTAwZWEwNTJhYjk3YjUzYWUiLCJ0YW5rIjpmYWxzZSwic2VxdWVuY2UiOjF9XSwianNvbiI6bnVsbCwiYWRkcmVzcyI6bnVsbCwib3V0cHV0cyI6bnVsbCwia2V5SW1hZ2VzIjpudWxsLCJ2MSI6bnVsbCwicjEiOm51bGwsInMxIjpudWxsLCJ2MiI6bnVsbCwicjIiOm51bGwsInMyIjpudWxsfQ=="
    }
  ]
}
```

### HTTP Request
`GET /:coin/wallets/:walletId/transferRequests?transferState=PENDING_APPROVAL`

### Response
Returns an array of Transfer Request Objects with transfer state of PENDING_APPROVAL. See [Get Transfer Request](#get-transfer-request) for the transfer request object.






## Approve Pending Approval
```json
curl "http://localhost:8657/api/pendingApprovals/5b47858edce04ac2a81613c4d349cf37/approve"
-H "API-KEY: 359c26a316f97e17bf6b17169e6bd816"
-H "API-KEY-PASSPHRASE: Xwings2019"
-H "API-KEY-SECRET: x6NzNCWvCNSNnM/60QxKyRBqR/cl9gVQoDSv3ssn9ZM="
-X "POST"
```

> Sample response:

```json
{
  "transferRequestId": "5b47858edce04ac2a81613c4d349cf37",
  "coin": "BTC",
  "walletId": "773988afc53347e48aa9100ac0c24d48",
  "toAddress": "2MsYKTgDCqy5HqrJxJFo3w9fpG63kGxRwFC",
  "amount": "0.0003",
  "transferState": "APPROVED",
  "approvalsRequired": 1,
  "createdTime": 1546927220768907,
  "createdBy": "8f1d99de6db74f948e22603bced34386"
}
```

Approve transfer request.

### HTTP Request
`POST /pendingApprovals/:transferRequestId/approve`

### Response
Returns the transfer request just approved. See [Get Transfer Request](#get-transfer-request) for the transfer request object.








## Reject Pending Approval Transfer Request
```json
curl "http://localhost:8657/api/pendingApprovals/35ec9d4e347745dfbf0e7ccec03679a8/reject"
-H "API-KEY: 359c26a316f97e17bf6b17169e6bd816"
-H "API-KEY-PASSPHRASE: Xwings2019"
-H "API-KEY-SECRET: x6NzNCWvCNSNnM/60QxKyRBqR/cl9gVQoDSv3ssn9ZM="
-X "POST"
```

> Sample response:

```json
{
  "transferRequestId": "35ec9d4e347745dfbf0e7ccec03679a8",
  "coin": "BTC",
  "walletId": "773988afc53347e48aa9100ac0c24d48",
  "toAddress": "2MsYKTgDCqy5HqrJxJFo3w9fpG63kGxRwFC",
  "amount": "0.0003",
  "transferState": "REJECTED",
  "approvalsRequired": 1,
  "createdTime": 1546939576505091,
  "createdBy": "8f1d99de6db74f948e22603bced34386"
}
```

Reject transfer request.

### HTTP Request
`POST /pendingApprovals/:transferRequestId/reject`

### Response
Returns the rejected transfer request. See [Get Transfer Request](#get-transfer-request) for the transfer request object.







## Get Transfer By TransferId
```json
curl "http://localhost:8657/api/BTC/wallets/b2993a9eb932437a9b742fa9f5267086/transfers/17c7d62781be4e0897ae0641b81d5a61"
-H "API-KEY: 359c26a316f97e17bf6b17169e6bd816"
-H "API-KEY-PASSPHRASE: Xwings2019"
-H "API-KEY-SECRET: x6NzNCWvCNSNnM/60QxKyRBqR/cl9gVQoDSv3ssn9ZM="
-X "GET"
```

> Sample response:

```json
{
  "transferId": "17c7d62781be4e0897ae0641b81d5a61",
  "coin": "BTC",
  "walletId": "773988afc53347e48aa9100ac0c24d48",
  "txid": "68d1b0d7e859695f369ff0650fd1c3ecb05f1a936850766bb89ecf6dfbf96111",
  "createdTime": 1546064458756020,
  "lastModifiedTime": 1546064458756020,
  "confirmations": 1358,
  "transferState": "CONFIRMED",
  "confirmedTime": 1546064458756001,
  "transferType": "SEND",
  "amount": "0.001",
  "fee": "0.00000444",
  "destinationAddress": "2N5pTPNTdofExnzzrd6R6CeMBneZKWExJ4V",
  "sourceAddress": "2N5pTPNTdofExnzzrd6R6CeMBneZKWExJ4V"
}
```

Returns wallet Transfer object.

### HTTP Request
`GET /:coin/wallets/:walletId/transfers/:transferId`

### Response
Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
transferId       | String                          | M           | Transfer id
coin             | String                          | M           | Coin id
walletId         | String                          | M           | Wallet id
txid             | String                          | M           | Txid on blockchain
createdTime      | Long                            | M           | Time the transfer was created
lastModifiedTime | Long                            | M           | Time the transfer was last updated
confirmations    | Integer                         | M           | Number of confirmations
transferState    | Enum                            | M           | Please refer to [transferState](#transfer-state) in enums file
confirmedTime    | Long                            | M           | Time the transfer was confirmed





## Get Transfer By Txid
```json
curl "http://localhost:8657/api/BTC/wallets/b2993a9eb932437a9b742fa9f5267086/transfers?txid=68d1b0d7e859695f369ff0650fd1c3ecb05f1a936850766bb89ecf6dfbf96111"
-H "API-KEY: 359c26a316f97e17bf6b17169e6bd816"
-H "API-KEY-PASSPHRASE: Xwings2019"
-H "API-KEY-SECRET: x6NzNCWvCNSNnM/60QxKyRBqR/cl9gVQoDSv3ssn9ZM="
-X "GET"
```

> Sample response:

```json
{
  "transferResponses": [
    {
      "transferId": "17c7d62781be4e0897ae0641b81d5a61",
      "coin": "BTC",
      "walletId": "773988afc53347e48aa9100ac0c24d48",
      "txid": "68d1b0d7e859695f369ff0650fd1c3ecb05f1a936850766bb89ecf6dfbf96111",
      "createdTime": 1546064458756020,
      "lastModifiedTime": 1546064458756020,
      "confirmations": 1358,
      "transferState": "CONFIRMED",
      "confirmedTime": 1546064458756001,
      "transferType": "SEND",
      "amount": "0.001",
      "fee": "0.00000444",
      "destinationAddress": "2N5pTPNTdofExnzzrd6R6CeMBneZKWExJ4V",
      "sourceAddress": "2N5pTPNTdofExnzzrd6R6CeMBneZKWExJ4V"
    }
  ]
}
```

### HTTP Request
`GET /:coin/wallets/:walletId/transfers?txid=:txid`
    
### Response
Returns an array of Transfer objects. See [Get Transfer By TransferId](#get-transfer-by-transferid) for the Transfer Object.







## Get All Transfers
```json
curl "http://localhost:8657/api/BTC/wallets/b2993a9eb932437a9b742fa9f5267086/transfers"
-H "API-KEY: 359c26a316f97e17bf6b17169e6bd816"
-H "API-KEY-PASSPHRASE: Xwings2019"
-H "API-KEY-SECRET: x6NzNCWvCNSNnM/60QxKyRBqR/cl9gVQoDSv3ssn9ZM="
-X "GET"
```

> Sample response:

```json
{
  "transferResponses": [
    {
      "transferId": "17c7d62781be4e0897ae0641b81d5a61",
      "coin": "BTC",
      "walletId": "773988afc53347e48aa9100ac0c24d48",
      "txid": "68d1b0d7e859695f369ff0650fd1c3ecb05f1a936850766bb89ecf6dfbf96111",
      "createdTime": 1546064458756020,
      "lastModifiedTime": 1546064458756020,
      "confirmations": 1358,
      "transferState": "CONFIRMED",
      "confirmedTime": 1546064458756001,
      "transferType": "SEND",
      "amount": "0.001",
      "fee": "0.00000444",
      "destinationAddress": "2N5pTPNTdofExnzzrd6R6CeMBneZKWExJ4V",
      "sourceAddress": "2N5pTPNTdofExnzzrd6R6CeMBneZKWExJ4V"
    },
    {
      "transferId": "8a52d81790b746c7a1cab2069d44471d",
      "coin": "BTC",
      "walletId": "773988afc53347e48aa9100ac0c24d48",
      "txid": "d145435bcfec7bd13d9f20e2f9af06decda6f6760dfe029d7f6be729fdf00977",
      "createdTime": 1546612279000941,
      "lastModifiedTime": 1546612279000941,
      "confirmations": 420,
      "transferState": "CONFIRMED",
      "confirmedTime": 1546612279000931,
      "transferType": "SEND",
      "amount": "0.01",
      "fee": "0.00000444",
      "destinationAddress": "2N7wgViXpGoVF19cfwEjNyJYTfCda9L7ccT",
      "sourceAddress": "2N5pTPNTdofExnzzrd6R6CeMBneZKWExJ4V"
    }
  ]
}
```

### HTTP Request
`GET /:coin/wallets/:walletId/transfers`
    
### Response
Returns an array of Transfer objects. See [Get Transfer By TransferId](#get-transfer-by-transferid) for the Transfer Object.



















# Webhook Notifications
Webhooks shall be set up to receive callbacks from DaGuard programmatically. They are attached to wallets and are triggered when an wallet event occurs.

DaGuard will make a POST http request to the URL defined in the webhook with a JSON payload, and expect a HTTP 200 OK. If a successful response is not received, DaGuard will attempt to retry the webhook with an increasing delay between each retry.

Since anyone on the Internet can send HTTP requests to the Webhook URL, the request body payload should not be trusted. Please verify any information sent in the webhook by fetching the transfer/block data from DaGuard before processing the notification.

Developers should take care to ensure that their application succeeds even in the cases of transient network error, or if receive the same webhook twice due to an improper acknowledgement.


## WebHook Types
Type                  | Description
----------------------|-----------------------
TRANSFER              | Activates when a transaction is seen/confirmed on block chain
PENDING_APPROVAL      | Activates when a pending approval on the user's wallet is created, approved, or rejected


## Transfer Webhook
DaGuard will look over digital coin block chain, when DaGuard detected a transactions, DaGuard will give a callback according to your webhook configuration.

### Transfer Webhook Object

Name             | Type(value)                | Mandatory   | Description
-----------------|----------------------------|-------------|-----------------------
wallet           | String                     | M           | ID of the wallet associated with the webhook event, if this is a wallet webhook
transfer         | String                     | M           | Transfer Id, Transfer ID, a DaGuard generated id of the transfer. This can be used to lookup more details about the transaction.
coin             | String                     | M           | Crypto Currency or Ethereum Token
type             | String                     | M           | Type of Webhook(Can be transfer, pendingapproval)
state            | String                     | M           | CONFIRMED

## Pending Approval Webhook
DaGuard will send Pending Approval Webhook when transfer requests were approved or rejected, also DaGuard will send email to tell you status changes.

### Pending Approval Webhook Object

Name                 | Type(value)                     | Mandatory   | Description
---------------------|---------------------------------|-------------|-----------------------
wallet               | String                          | M           | ID of the wallet associated with the webhook event, if this is a wallet webhook
transferRequestId    | String                          | M           | Transfer Request Id, Transfer Request ID, a DaGuard generated id of the transfer Request. This can be used to lookup more details about the transfer request.
coin                 | String                          | M           | Crypto Currency or Ethereum Token
type                 | String                          | M           | Type of Webhook(Can be transfer, pendingapproval)
state                | String                          | M           | APPROVED/REJECTED


## Create WebHook
DaGuard support configuration Webhook through Local DaGuard Station.

```json
curl "https://localhost:8657/api/wallets/b2993a9eb932437a9b742fa9f5267086/webhooks"
-H "API-KEY: 359c26a316f97e17bf6b17169e6bd816" 
-H "API-KEY-PASSPHRASE: Xwings2019" 
-H "API-KEY-SECRET: x6NzNCWvCNSNnM/60QxKyRBqR/cl9gVQoDSv3ssn9ZM="
-X "POST"
-H "Content-Type:application/json"
-d '{"type":"TRANSFER","url":"http://www.example.com/hook"}'
```

> Sample response:

```json
{
  "walletId": "b2993a9eb932437a9b742fa9f5267086",
  "type": "TRANSFER",
  "url": "http://www.example.com/hook",
  "version": 1,
  "createdTime": 1546941666256262
}
```

### HTTP Request
`Post /wallets/:walletId/webhooks`

### Body Parameters
Name                     | Type(value)       | Mandatory   | Description
-------------------------| ------------------|-------------|-----------------------
type                     | String            | M           | webhook type, PENDING_APPROVAL/TRANSFER
url                      | String            | M           | accessible host to accept notification

### Response
The webhook created to wallet


## Get Wallet All WebHooks
Get All WebHooks by WalletId

```json
curl "https://localhost:8657/api/wallets/b2993a9eb932437a9b742fa9f5267086/webhooks"
-H "API-KEY: 359c26a316f97e17bf6b17169e6bd816" 
-H "API-KEY-PASSPHRASE: Xwings2019" 
-H "API-KEY-SECRET: x6NzNCWvCNSNnM/60QxKyRBqR/cl9gVQoDSv3ssn9ZM="
-X "GET"
```

> Sample response:

```json
{
  "webHooks": [
    {
      "walletId": "7378a51735364602be93b80c2dd3d8dc",
      "type": "TRANSFER",
      "url": "http://www.example.com/hook",
      "version": 1,
      "createdTime": 1551174100076418
    },
    {
      "walletId": "7378a51735364602be93b80c2dd3d8dc",
      "type": "PENDING_APPROVAL",
      "url": "http://www.example.com/hook",
      "version": 1,
      "createdTime": 1551174107021635
    }
  ]
}
```

### HTTP Request
`Get /wallets/:walletId/webhooks`

### Response
Return List of Web Hook: webHooks.

Name                 | Type(value)                     | Mandatory   | Description
---------------------|---------------------------------|-------------|-----------------------
wallet               | String                          | M           | ID of the wallet associated with the webhook event, if this is a wallet webhook
transferRequestId    | String                          | M           | Transfer Request Id, Transfer Request ID, a DaGuard generated id of the transfer Request. This can be used to lookup more details about the transfer request.
coin                 | String                          | M           | Crypto Currency or Ethereum Token
type                 | String                          | M           | Type of Webhook(Can be transfer, pendingapproval)
state                | String                          | M           | APPROVED/REJECTED



## Delete Wallet WebHook
```json
curl "https://localhost:8657/api/wallets/b2993a9eb932437a9b742fa9f5267086/webhooks"
-H "API-KEY: 359c26a316f97e17bf6b17169e6bd816" 
-H "API-KEY-PASSPHRASE: Xwings2019" 
-H "API-KEY-SECRET: x6NzNCWvCNSNnM/60QxKyRBqR/cl9gVQoDSv3ssn9ZM="
-X "DELETE"
-d "{\"type\": \"PENDING_APPROVAL\",\"url\": \"http://www.example.com/hook\"}"
```

> Sample response:

```json
{
  "success": true
}
```

### HTTP Request
`Delete /wallets/:walletId/webhooks`

### Body Parameters
Name                     | Type(value)       | Mandatory   | Description
-------------------------| ------------------|-------------|-----------------------
type                     | String            | M           | webhook type, PENDING_APPROVAL/TRANSFER
url                      | String            | M           | accessible host to accept notification

### Response
Return delete Webhook result

Name                     | Type(value)       | Mandatory   | Description
-------------------------| ------------------|-------------|-----------------------
success                  | Boolean           | M           | delete Webhook result, can be true or false
















# Enums

## Transfer State
Transfer State           | Description
-------------------------| --------------------------------------------------
CONFIRMED                | Transfer has been confirmed
UNCONFIRMED              | Transfer has not been confirmed
PENDING_APPROVAL         | Transfer request is in pending subject to approval
REJECTED                 | Transfer request is rejected















# Error Codes

Error Code                              | Description
----------------------------------------| ---------------------------------------
 INTERNAL_SERVER_ERROR                  | Internal server error
 INVALID_EMAIL_FORMAT                   | Invalid email format
 BAD_PASSWORD                           | Password doesn't meet requirement
 INVALID_CONTACT_NUMBER                 | Invalid contact phone number
 INVALID_ACTIVATION_LINK                | Invalid account activation link
 INVALID_RESET_PASSWORD_LINK            | Invalid reset password link
 INVALID_AUTHENTICATION                 | Invalid username or password 
 ORGANIZATION_IS_EXISTED                | The organization name has been registered
 USER_EAMIL_IN_USE                      | The email has been registered
 USER_USERNAME_IN_USE                   | The username has been registered
 USER_NOT_FOUND                         | Invalid account
 USER_NOT_ACTIVATED                     | The account has been registered but activated 
 USER_DISABLED                          | The account is disabled
 PASSWORD_SAME_TO_PREVIOUS              | New password is same to previous
 TWO_FACTOR_IS_ACTIVATED                | Two factor authentication has been activated
 INVALID_TWO_FACTOR_CODE                | Invalid two factor code
 TWO_FACTOR_NOT_ACTIVATED               | Two factor authentication is not activated
 APIKEY_NICKNAME_EXISTED                | Apikey nickname has exsited
 APIKEY_NOT_FOUND                       | Invalid apikey
 USER_WALLET_NOT_FOUND                  | Wallet not found under the account
 APIKEY_EXCEED_USER_WALLET_ACCESS_LEVEL | Apikey access level to wallet beyond user access level 
 APIKEY_WALLET_EMPTY                    | Apikey creation should contain at least one wallet
 APIKEY_DISABLED                        | Apikey is disabled
 USER_IS_ACTIVATED                      | The account has already been activated

