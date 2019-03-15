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


