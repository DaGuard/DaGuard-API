# ui only api
                             
* [Register](#register)
* [Activate](#activate)
* [Login](#login)
* [Logout](#logout)
* [Forgot password](#forgot-password)
* [Verify forgot password](#verify-forgot-password)
* [Reset password](#reset-password)
* [Update profile](#update-profile)
* [Change password](#change-password)
* [Activate two factor](#activate-two-factor)
* [Update two factor](#update-two-factor)
* [Get two factor secret](#get-two-factor-secret)
* [Get two factor settings](#get-two-factor-settings)
* [Get self](#get-self)
* [Create apikey](#create-apikey)
* [Delete apikey](#delete-apikey)
* [Get apikeys](#get-apikeys)
* [Create tank](#create-tank)
* [Get tanks](#get-tanks)
* [Get policyRules](#get-policyrules)
* [Create policyRule](#create-policyrule)
* [Create WebHook](#createWebHook)
* [List WebHooks](#listWebHooks)
* [Delete WebHook](#deleteWebHook)
* [Invite user](#inviteUser)
* [Disable user](#diableUser)
* [Enable user](#enableUser)
* [Get organization users](#getOrganizationUsers)
* [Verify invitation url](#verifyInvitationUrl)
* [Reset invited user password](#resetInvitedUserPassword)
* [Resend invitation url](#resendInvitationUrl)
* [Get wallet users](#getWalletUsers)
* [Add wallet user](#addWalletUser)
* [Remove wallet user](#removeWalletUser)

<a name="register"/>                
## Register                 

    POST /user/register
    
### Request parameters

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
organizationName | String                          | M           | 
contactNumber    | String                          | M           | 
email            | String                          | M           | 
firstName        | String                          | M           | 
lastName         | String                          | M           | 
password         | String                          | M           | 

### Success response

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
messageCode      | String                          | M           | CHECK_EMAIL_TO_CONFIRM


<a name="activate"/>                
## Activate                 

    GET /user/activate/:email/:token
  
### Success response

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
sessionToken     | String                          | M           | 



<a name="login"/>                   
## Login                    

    POST /user/login

### Request parameters
  
Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
email            | String                          | M           | 
password         | String                          | M           | 

### Success response

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
sessionToken     | String                          | M           | 


<a name="logout"/>                  
## Logout                   

    POST /user/logout
  

### Success response

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
status           | Boolean                         | M           | 


<a name="forgot-password"/>         
## Forgot password          

    POST /user/forgot-password

### Request parameters
  
Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
email            | String                          | M           | 


### Success response

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
messageCode      | String                          | M           | CHECK_EMAIL_TO_RESET_PASSWORD



<a name="verify-forgot-password"/>  
## Verify forgot password   

    GET /user/verify-forgot-password/:email/:token
  

### Success response

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
status           | Boolean                         | M           | 



<a name="reset-password"/>          
## Reset password           

    POST /user/reset-password
  
### Request parameters
  
Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
email            | String                          | M           | 
password         | String                          | M           | 
token            | String                          | M           | 


### Success response

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
status           | Boolean                         | M           | 


<a name="update-profile"/>          
## Update profile           

    POST /user/update-profile
    
### Request parameters

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
username         | String                          | M           | 


### Success response

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
status           | Boolean                         | M           | 


<a name="change-password"/>         
## Change password          

    POST /user/change-password
    
### Request parameters
  
Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
password         | String                          | M           | 
oldPassword      | String                          | M           | 

### Success response

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
status           | Boolean                         | M           | 



<a name="activate-two-factor"/>     
## Activate two factor      

    POST /user/two-factor/activate
    
### Request parameters
  
Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
secret           | String                          | M           | 
code             | String                          | M           | 

### Success response

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
enabled          | Boolean                         | M           | 
authorities      | Array                           | M           | Array of two factor authorities


<a name="update-two-factor"/>       
## Update two factor        

    POST /user/two-factor/update
  
### Request parameters

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
enabled          | Boolean                         | M           | 
authorities      | Array                           | M           | Array of two factor authorities

### Success response

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
status           | Boolean                         | M           | 

<a name="get-two-factor-secret"/>   
## Get two factor secret    

    GET /user/two-factor/secret

### Success response
  
Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
username         | String                          | M           | 
secret           | String                          | M           | 




<a name="get-two-factor-settings"/> 
## Get two factor settings  

    GET /user/two-factor/settings

### Success response

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
enabled          | Boolean                         | M           | 
authorities      | Array                           | M           | Array of two factor authorities



<a name="get-self"/>                
## Get self                 

    GET /user/self
  

### Success response
  
Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
email            | String                          | M           | 
username         | String                          | M           | 
twoFactorEnabled | Boolean                         | M           | 
organizationId   | String                          | M           |
organizationName | String                          | M           |
userRole         | String                          | M           |


<a name="create-apikey"/>           
## Create apikey            

    POST /user/apikeys
  
### Request parameters

Name              | Type(value)                     | Mandatory   | Description
------------------| --------------------------------|-------------|-----------------------
apiPassphrase     | String                          | M           | 
nickname          | String                          | M           | 
accessLevel       | String                          | M           | String value of access level
spendLimits       | Json Object                     | M           | Map of coin and spend limit value, e.g. {"BTC": 1000}
ipAddressWhitelist| Array                           | M           | Array of ip addresses

### Success response
  
Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
apikey           | String                          | M           | 
apiSecret        | String                          | M           | 
enabled          | Boolean                         | M           | 


<a name="delete-apikey"/>           
## Delete apikey            

    DELETE /user/apikeys/:apikey
  
### Success response

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
status           | Boolean                         | M           | 


<a name="get-apikeys"/>             
## Get apikeys              

    GET /user/apikeys

### Success response

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|----------------------------
apikeys          | Array                           | M             | Array of apikey json object  

### Apikey object

Name              | Type(value)                     | Mandatory   | Description
----------------- | --------------------------------|-------------|----------------------------
apikey            | String                          | M           |
nickname          | String                          | M           | 
enabled           | Boolean                         | M           | 
accessLevel       | String                          | M           | String value of access level
spendLimits       | Json Object                     | M           | Map of coin and spend limit value, e.g. {"BTC": 1000}
ipAddressWhitelist| Array                           | M           | Array of ip addresses

<a name="create-tank"/>           
## Create tank            

    POST /organizations/:organizationId/tanks
  
### Request parameters

Name              | Type(value)                     | Mandatory   | Description
------------------| --------------------------------|-------------|-----------------------
coin              | String                          | M           | 
minBalance        | DoubleString                    | O           | Tank min balance
maxBalance        | DoubleString                    | O           | Tank max balance

### Success response

Returns Tank object.

### Tank Fields

<a name="tank" id="tank"> </a>
  
Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
coin             | String                          | M           | 
address          | String                          | M           | 
balance          | DoubleString                    | M           | Tank balance
minBalance       | DoubleString                    | M           | Tank min balance
maxBalance       | DoubleString                    | M           | Tank max balance

<a name="get-tanks"/>           
## Get tanks            

    GET /organizations/:organizationId/tanks  

### Success response

Returns an array of Tank objects.

### Tank Body Fields

Please refer to [Tank](#tank) object

<a name="get-policyrules" id="get-policyrules"> </a>
---
## Get policyRules

	GET /:coin/wallets/:walletId/policyRule
	
### Success response

Array of PolicyRule Object

### PolicyRule Object

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
id               | String                          | M           | 
coin             | String                          | M           | 
action           | String                          | M           | e.g. "DENY", "GET_APPROVAL"
condition        | String                          | M           | e.g. {"address": ["string"], "amount": 1, "timeWindow": 0}
walletPolicyId   | String                          | M           | 

<a name="create-policyrule" id="create-policyrule"> </a>
---
## Create policyRule

	POST /:coin/wallets/:walletId/policyRule
	
### Request parameters

Name              | Type(value)                     | Mandatory   | Description
------------------| --------------------------------|-------------|-----------------------
action            | String                          | M           | e.g. "DENY", "GET_APPROVAL"
condition         | String                          | M           | e.g. {"address": ["string"], "amount": 1, "timeWindow": 0}
type              | String                          | M           | PolicyRuleType e.g. "VELOCITY_LIMIT", "COIN_ADDRESS_WHITE_LIST" or "COIN_ADDRESS_BLACK_LIST"

### Success response

Return PolicyRule Object
	
	
<a name="createWebHook" id="createWebHook"> </a>
---
## Create WebHook
    Post /wallets/:walletId/webhooks
create a webHook for wallet

### Request Parameters

Name             | Type(value)                     | Mandatory   | Description
---------------| ---------------------------|-----------|-----------------------
type           | String                     | M           | TRANSFER/PENDING_APPROVAL
version        | Integer                     | M           | Number of version
url            | String                    | M           | web hook destination url

<a name="webHook" id="webHook"> </a>
---
### WebHook Object Fields
Name             | Type(value)                     | Mandatory   | Description
---------------| ---------------------------|-----------|-----------------------
walletId       | String                     | M           | wallet id
type           | String                     | M           | TRANSFER/PENDING_APPROVAL
url            | String                     | M           | web hook destination url
version        | Integer                    | M           | Number of version
createdTime    | Long                       | M           | Time of create web hook

<a name="listWebHooks" id="listWebHooks" > </a>
---
## List WebHooks
    Get /wallets/:walletId/webhooks
Returns Web Hook List Object, please refer to [WebHook](#webHook)

<a name="deleteWebHook" id="deleteWebHook" > </a>
---
## Delete WebHook
    DELETE /wallets/:walletId/webhooks
    
### Request Parameters

Name             | Type(value)              | Mandatory   | Description
---------------| ---------------------------|-------------|-----------------------
type           | String                     | M           | TRANSFER/PENDING_APPROVAL
url            | String                     | M           | web hook destination url


<a name="inviteUser"> </a>                
## Invite user

    POST /user/invite
    
### Request parameters

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
email            | String                          | M           | 
firstName        | String                          | M           | 
lastName         | String                          | M           | 
userRole         | String                          | M           | 

### Success response

Returns Organization user object.
<a name="organizationUser" id="organizationUser"> </a>

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
email            | String                          | M           | 
firstName        | String                          | M           | 
lastName         | String                          | M           | 
userRole         | String                          | M           | 
isActivated      | boolean                         | M           | 
enabled          | boolean                         | M           | 
isOwner          | boolean                         | M           | 

---
<a name="diableUser"> </a>                
## Disable user

    POST /user/disable
    
### Request parameters

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
email            | String                          | M           | 

### Success response

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
status           | boolean                         | M           | 


---
<a name="enableUser"> </a>                
## Enable user

    POST /user/enable
    
### Request parameters

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
email            | String                          | M           | 

### Success response

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
status           | boolean                         | M           | 


---
<a name="getOrganizationUsers"> </a>                
## Get organization users

    GET /user/organization-users
    

### Success response

Name             | Type(value)                                         | Mandatory   | Description
-----------------| ----------------------------------------------------|-------------|---------
organizationUsers| Array of [organization user](#organizationUser)     | M           |


---
<a name="verifyInvitationUrl"> </a>                
## Verify invitation url

    GET /user/verify-invited-user/:email/:token
    
### Success response

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
status           | boolean                         | M           | 


---
<a name="resetInvitedUserPassword"> </a>                
## Reset invited user password

    POST /user/reset-invited-user-password
    
### Request parameters

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
email            | String                          | M           | 
password         | String                          | M           | 
token            | String                          | M           | 

### Success response

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
status           | boolean                         | M           |


---
<a name="resendInvitationUrl"> </a>                
## Resend invitation url

    POST /user/resend-invitation-url
    
### Request parameters

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
email            | String                          | M           | 

### Success response

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
status           | boolean                         | M           | 

---
<a name="getWalletUsers"> </a>                
## Get wallet users

    GET /user/wallet-users/:walletId
    
### Success response

Name             | Type(value)                         | Mandatory   | Description
-----------------| ------------------------------------|-------------|-----------------------
walletUsers      | Array of [Wallet user](#walletUser) | M           |

<a name = "walletUser"> </a>
Wallet user object fields

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
email            | String                          | M           | 
firstName        | String                          | M           | 
lastName         | String                          | M           | 
accessLevel      | String                          | M           | 


---
<a name="addWalletUser"> </a>                
## Add wallet user

    POST /user/wallet-users/:walletId

### Request parameters

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
emails           | Array of email strings          | M           | 
accessLevel      | String                          | M           | 
    
### Success response

Name             | Type(value)                         | Mandatory   | Description
-----------------| ------------------------------------|-------------|-----------------------
walletUsers      | Array of [Wallet user](#walletUser) | M           |


---
<a name="removeWalletUser"> </a>                
## Remove wallet user

    DELETE /user/wallet-users/:walletId

### Request parameters

Name             | Type(value)                     | Mandatory   | Description
-----------------| --------------------------------|-------------|-----------------------
email            | String                          | M           | 
    
### Success response

Name             | Type(value)                         | Mandatory   | Description
-----------------| ------------------------------------|-------------|-----------------------
status           | boolean                             | M           |
	