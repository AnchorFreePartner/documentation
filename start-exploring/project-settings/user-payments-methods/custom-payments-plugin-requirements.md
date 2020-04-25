---
description: Description and requirements of a user payments plugin.
---

# Payments Plugin requirements

You need a payment plugin if your application uses another payment service, not supported in the Platform side payment methods.

AnchorFree VPN SDK: Purchase API guide

## Payment Flow

**Step 1.** Your App made a subscription in your Payment service and get a purchase receipt.

**Step 2.** Send ****the ****_purchase receipt_ to the Platform side:

1. the App call POST [`/user/purchase`](https://backend.northghost.com/doc/all/index.html#!/user-controller/sendPurchase) \(SDK include the same method\) with parameters `token = your purchase receipt` and `type = name your plagin`.
2. your Backend call [POST](https://backend.northghost.com/doc/all/index.html#!/partner-controller/sendPurchaseByPartner) [`/partner/subscribers/{user_id}/purchase`](https://backend.northghost.com/doc/all/index.html#!/partner-controller/sendPurchaseByPartner) with parameters `body = your purchase receipt` and `user_id = the user ID`.

**Step 3.** The Platform verifies the purchase receipt in your Payment service. 

* If the result _Failed_, the Platform:
  * returns the error code. 
* If the result _Success_, the Platform:
  * changes the user status to _Paid_ ,
  * changes the user bandwidth limit to _Unlimited,_
  * send to App _Result._

**Step 4.**  The Platform will check check the _Purchase receipt_ each 24 hours.

* If the result _Success_, the Platform:
  * does nothing.
* If the result _Failed_, the Platform:  
  * changes the user status to _Free_ ,
  * changes the user bandwidth limit to _Free limit = 100Mb._

## Purchase APIs details

### 

### Server side: Add purchase

POST:

[https://backend.northghost.com/partner/subscribers/{user\_id}/purchase](https://backend.northghost.com/partner/subscribers/%7buser_id%7d/purchase)

Parameters

| Field name | Type | quantity | Max length | Mandatory | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| user\_id | integer | 1..1 | 64 | Yes | Unique user ID for AFB |
| access\_token |  |  |  | Yes | Unique token for partner to access the API. Expire every 24 hours |
| body | object |  |  | Yes | Details of valid purchase associated with the user |

Body JSON object detail

| Field name | Type | quantity | Max length | Description |
| :--- | :--- | :--- | :--- | :--- |
| purchase\_info | object |  |  | Purchase vendor specific data about the purchase, such as receipt |
| user\_info | object |  |  | User’s bandwidth limit and licence ID to determine user status and plan |
| Ticket | object |  |  | Raw JSON ticket/ receipt of the purchase. “orderId” will be used as a unique key for each subscription |
| Type | String |  |  | Payment type description \(“general”\) |
| active\_timestamp | Number, Long | 1..1 | 13 | Active time for current paid subscription period |

body format

```text
"user_info": {
 "bandwidth_limit": "500000000",
 "license_id": 1
},
"purchase_info": {
 "ticket": {
 "orderId":"1299976ABC3169054705758ABC",
 "transactionId":"1299976ABC3169054705758ABC",
 "purchaseTime":1345678900000,
 "expireTime":167890000000,
 "purchaseState":0,
 "purchaseToken":"rojeslcdyyiapnqcynkjyyjh"
 “trialLength”: 7
 “duration”: 30
 “usdAmount”: 7.99
 “originalPurchaseTime”:123445000,
 “planName”: “abc_yearly_trial_2999”
 “environment”:”production”
 “purchaseHistory”: [
 {
 “transactionId”:”12FJR4TR123456”,
 "purchaseTime":1345678900000,
 "expireTime":167890000000,
 "purchaseState":0,
 "purchaseToken":"rojeslcdyyiapnqcynkjyyjh"
 },
 {(all transaction history)
 }
 ]
 },
 "type": "general_bitdefender",
}
```



purchase\_info “ticket” detail

<table>
  <thead>
    <tr>
      <th style="text-align:left">Field name</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">quantity</th>
      <th style="text-align:left">Max length</th>
      <th style="text-align:left">Mandatory</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">orderId</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">Unique identifier for the subscription which should not change upon renewal.
        This ID is used to verify purchase.</td>
    </tr>
    <tr>
      <td style="text-align:left">transactionId</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Yes (for auto renewals)</td>
      <td style="text-align:left">Unique identifier for each transaction (purchase), if the payment system
        sends different IDs for different transactions.</td>
    </tr>
    <tr>
      <td style="text-align:left">purchaseTime</td>
      <td style="text-align:left">Long</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">Unix timestamp when the most recent transaction occurred for the subscription</td>
    </tr>
    <tr>
      <td style="text-align:left">expireTime</td>
      <td style="text-align:left">Long</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">Unix timestamp when the most recent period will expire</td>
    </tr>
    <tr>
      <td style="text-align:left">purchaseState</td>
      <td style="text-align:left">Int</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">
        <p>0: Successful paid transaction, 1: Refunded transaction, 2: Free transaction
          (trial)</p>
        <p>If it&#x2019;s null, assume it is a successful paid transaction.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">purchaseToken</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">Optional field to put any token/receipt string</td>
    </tr>
    <tr>
      <td style="text-align:left">trialLength</td>
      <td style="text-align:left">Int</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">Number of days of free trial for the subscription. 0: No trial</td>
    </tr>
    <tr>
      <td style="text-align:left">duration</td>
      <td style="text-align:left">Int</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">Subscription&#x2019;s renewal cycle in days. It can either be static number
        of reflect actual duration of the most recent period.</td>
    </tr>
    <tr>
      <td style="text-align:left">usdAmount</td>
      <td style="text-align:left">Float</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">User facing unit price of the subscription in USD. It is not mandatory
        but it is very important to have this. If it is trial, it should be 0.</td>
    </tr>
    <tr>
      <td style="text-align:left">originalPurchaseTime</td>
      <td style="text-align:left">Long</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">UNIX timestamp when the first transaction made for the subscription (new
        purchase or trial start)</td>
    </tr>
    <tr>
      <td style="text-align:left">planName</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">Plan or SKU name of the subscription for reference</td>
    </tr>
    <tr>
      <td style="text-align:left">environment</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">&#x201C;Production&#x201D; or &#x201C;Test&#x201D;. If null, it is assumed
        as a production (real) purchase.</td>
    </tr>
    <tr>
      <td style="text-align:left">purchaseHistory</td>
      <td style="text-align:left">array</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">
        <p>Store all transactions happened, i.e., new purchases and renewals, for
          the subscription (orderId).</p>
        <p>If there is purchaseHistory, transactionId and purchaseTime are mandatory.</p>
      </td>
    </tr>
  </tbody>
</table>Response

| Field name | Type | quantity | Max length | Description |
| :--- | :--- | :--- | :--- | :--- |
| purchase\_id | integer | 1..1 | 64 | Unique ID for each purchase for the user |

### Server side: Delete purchase

DELETE:

[https://backend.northghost.com/partner/subscribers/{user\_id}/purchase](https://backend.northghost.com/partner/subscribers/%7buser_id%7d/purchase)

Parameters

| Field name | Type | quantity | Max length | Mandatory | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| user\_id | integer | 1..1 | 64 | Yes | Unique user ID in AFB |
| access\_token |  |  |  | Yes | Unique token for partner to access the API. Expire every 24 hours |
| purchase\_id | integer | 1..1 | 64 | Yes | AnchorFree Unique ID for each purchase for the user. Sent as a response back when a purchase is added to a user |
| purchase\_info | object |  |  | No | Append the latest purchase\_info for the to be deleted purchase. It is important to change the purchaseState appropriately especially for refund. |

## Partner side APIs detail

Partner should prepare for the following APIs.

### Verify user

AFB will call this POST method to verify the token passed by the client.

Parameters

| Field name | Type | quantity | Max length | Description | Mandatory |
| :--- | :--- | :--- | :--- | :--- | :--- |
| token | string | 1..1 | 141 | OAuth token | Yes |
| vpn\_device\_id | String | 1..1 | 64 | Unique deviceId in the AnchorFree system | No \(depending on partner\) |

Response

<table>
  <thead>
    <tr>
      <th style="text-align:left">Field name</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">quantity</th>
      <th style="text-align:left">Max length</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Mandatory</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">is_valid</td>
      <td style="text-align:left">Boolean</td>
      <td style="text-align:left">1..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Whether the token is valid or not. Possible values: true/false</td>
      <td
      style="text-align:left">No</td>
    </tr>
    <tr>
      <td style="text-align:left">partner_user_id</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">1..1</td>
      <td style="text-align:left">64</td>
      <td style="text-align:left">
        <p>Unique user id generated by partner.</p>
        <p>For an invalid user, this would be set to -1</p>
      </td>
      <td style="text-align:left">Yes</td>
    </tr>
    <tr>
      <td style="text-align:left">user_info</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">1..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Details of current user parameters</td>
      <td style="text-align:left">No</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>purchase_info</p>
        <p>(See previous section for details)</p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">This will be used to add a new purchase to the user. For free users without
        any purchases, this will be empty</td>
      <td style="text-align:left">No* (Need the field for paid users)</td>
    </tr>
  </tbody>
</table>User info details

<table>
  <thead>
    <tr>
      <th style="text-align:left">Field name</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">quantity</th>
      <th style="text-align:left">Max length</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">bandwidth_limit</td>
      <td style="text-align:left">Number, Long</td>
      <td style="text-align:left">1..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>bandwidth limit for the user, in bytes.</p>
        <p>If unlimited, this is Null</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">license_id</td>
      <td style="text-align:left">Number, short</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>ID to determine number of devices allowed for the users.</p>
        <p>If unlimited, 1</p>
      </td>
    </tr>
  </tbody>
</table>response format example

```text
"is_valid": true,
"partner_user_id": “usernameofyourservice”,
"user_info": {
 "bandwidth_limit": Null, // Null gives unlimited bandwidth
 "license_id": 1 //1 gives 10,000 devices, which we consider unlimited
},
"purchase_info": {
 "ticket": {
 "orderId":"1299976ABC3169054705758ABC", //This is the ID for the subscription
 "transactionId":"1299976ABC3169054705758ABC", //If renewal happened, keep the orderId while sending a purchase with new transactionId
 "purchaseTime":1345678900000, //Time of the latest transaction. Changes in every renewal.
 "expireTime":167890000000,
 "purchaseState":0,
 "purchaseToken":"rojeslcdyyiapnqcynkjyyjh"
 “trialLength”: 0
 “duration”: 30
 “usdAmount”: 7.99
 “originalPurchaseTime”:123445000, //Time of the FIRST purchase. This does not change even for renewal transaction.
 “planName”: “abc_yearly_trial_2999”
 “environment”: “production”
 “purchaseHistory”: [
 {
 “transactionId”:”12FJR4TR123456”,
 "purchaseTime":1345678900000,
 "expireTime":167890000000,
 "purchaseState":0,
 "purchaseToken":"rojeslcdyyiapnqcynkjyyjh"
 },
 {(all transaction history)
 }
 ]
 },
 "type": "general_bitdefender",
}
```

### Verify purchase

AFB will call this POST method to verify the purchase when it’s first passed, and daily.

Parameters

| Field name | Type | Quantity | Max length | Description | Mandatory |
| :--- | :--- | :--- | :--- | :--- | :--- |
| partner\_user\_id | string | 1..1 | 64 | Unique user id generated by partner | Yes |
| purchase\_info |  |  |  | Details of the purchase to be verified. “orderId” inside “ticket” parameter must be present and is used as unique identifier for the verification | Yes |

Response

| Field name | Type | quantity | Max length | Description | Mandatory |
| :--- | :--- | :--- | :--- | :--- | :--- |
| is\_valid | Boolean | 1..1 |  | Whether the purchase is valid or not. Possible values: true/false | Yes |
| user\_info |  | 1..1 |  | Details of current user parameters | No |

