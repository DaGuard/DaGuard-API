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