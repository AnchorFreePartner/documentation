---
description: Description and requirements of a user payments plugin.
---

# Payments Plugin requirements

You need a payment plugin if your application uses another payment service, not supported in the Platform side payment methods.

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
  * send to App _purchase\_id._

**Step 4.**  The Platform will check check the _Purchase receipt_ each 24 hours.

* If the result _Success_, the Platform:
  * does nothing.
* If the result _Failed_, the Platform:  
  * changes the user status to _Free_ ,
  * changes the user bandwidth limit to _Free limit = 100Mb._

## Purchase receipt example

Purchase receipt should be in JSON format and include next details:

| Field name | Type | Description |
| :--- | :--- | :--- |
| purchase\_info | object | Purchase vendor specific data about the purchase, such as receipt |
| receipt | object | Raw JSON receipt of the purchase. “orderId” will be used as a unique key for each subscription |
| active\_timestamp | Number, Long | Active time for current paid subscription period |

body format

```text
"receipt": {
  "orderId": "1299976ABC3169054705758ABC",
  "transactionId": "1299976ABC3169054705758ABC",
  "purchaseTime": 1345678900000,
  "expireTime": 167890000000,
  "purchaseState": 0,
  “trialLength”: 7,
  “usdAmount”: 7.99,
  “originalPurchaseTime”: 123445000,
  “planName”: “abc_yearly_trial_2999”,
  "type": "mcafee"
}
```

purchase\_info “_receipt_” detail

<table>
  <thead>
    <tr>
      <th style="text-align:left">Field name</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">orderId</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">Unique identifier for the subscription which should not change upon renewal.
        This ID is used to verify purchase.</td>
    </tr>
    <tr>
      <td style="text-align:left">transactionId</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">Unique identifier for each transaction (purchase), if the payment system
        sends different IDs for different transactions.</td>
    </tr>
    <tr>
      <td style="text-align:left">purchaseTime</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">Unix timestamp when the most recent transaction occurred for the subscription</td>
    </tr>
    <tr>
      <td style="text-align:left">expireTime</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">Unix timestamp when the most recent period will expire</td>
    </tr>
    <tr>
      <td style="text-align:left">purchaseState</td>
      <td style="text-align:left">int</td>
      <td style="text-align:left">
        <p>0: Successful paid transaction, 1: Refunded transaction, 2: Free transaction
          (trial)</p>
        <p>If it&#x2019;s null, assume it is a successful paid transaction.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">trialLength</td>
      <td style="text-align:left">int</td>
      <td style="text-align:left">Number of days of free trial for the subscription. 0: No trial</td>
    </tr>
    <tr>
      <td style="text-align:left">usdAmount</td>
      <td style="text-align:left">float</td>
      <td style="text-align:left">User facing unit price of the subscription in USD. It is not mandatory
        but it is very important to have this. If it is trial, it should be 0.</td>
    </tr>
    <tr>
      <td style="text-align:left">originalPurchaseTime</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">UNIX timestamp when the first transaction made for the subscription (new
        purchase or trial start)</td>
    </tr>
    <tr>
      <td style="text-align:left">planName</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">Plan or SKU name of the subscription for reference</td>
    </tr>
    <tr>
      <td style="text-align:left">type</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">Payment Plugin name</td>
    </tr>
  </tbody>
</table>## Server side: Delete purchase

For delete a purchase you need to call API method DELETE:

[https://backend.northghost.com/partner/subscribers/{user\_id}/purchase](https://backend.northghost.com/partner/subscribers/%7buser_id%7d/purchase)

with next parameters:

| Field name | Type | Mandatory | Description |
| :--- | :--- | :--- | :--- |
| user\_id | integer | Yes | Unique user ID in the Platform |
| access\_token | string | Yes | Unique token for partner API. Expire every 24 hours. |
| purchase\_id | integer | Yes | Platform purchase ID of the user. Sent as a response back when a purchase is added to a user. |
| purchase\_info | object | No | Append the latest _purchase\_info_ for the to be deleted purchase. It is important to change the _purchaseState_ appropriately especially for refund. |

## Purchase receipt verification

Platform will call this POST method to verify the purchase \(see **Steps 3-4** on the Flow\) when it’s first passed, and daily.

**Parameters**

| Field name | Type | Description | Mandatory |
| :--- | :--- | :--- | :--- |
| partner\_user\_id | string | Unique user id generated by partner | Yes |
| purchase\_info | string | “orderId” must be present and is used as unique identifier for the verification | Yes |

**Response**

| Field name | Type | Description | Mandatory |
| :--- | :--- | :--- | :--- |
| is\_valid | Boolean | Whether the purchase is valid or not. Possible values: true/false | Yes |
| user\_info | Object | Details of current user parameters | No |

