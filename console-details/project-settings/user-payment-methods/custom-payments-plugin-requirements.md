---
description: Learn the description and requirements of the user payment plugin
---

# Payments Plugin requirements

You need a payment plugin if your application uses another payment service, not supported by the Platform.

## Payment Flow

**Step 1.** Your App buys a subscription in your Payment service and gets a purchase receipt.

**Step 2.** Send **** the **** _purchase receipt_ to the Platform side:

1. the App calls POST [`/user/purchase`](https://backend.northghost.com/doc/all/index.html#!/user-controller/sendPurchase) (SDK includes the same method) with parameters `token = your purchase receipt` and `type = name your plagin`.
2. your Backend calls [POST](https://backend.northghost.com/doc/all/index.html#!/partner-controller/sendPurchaseByPartner) [`/partner/subscribers/{user_id}/purchase`](https://backend.northghost.com/doc/all/index.html#!/partner-controller/sendPurchaseByPartner) with parameters `body = your purchase receipt` and `user_id = the user ID`.

**Step 3.** The Platform verifies the purchase receipt in your Payment service.&#x20;

* If the result is _Failed_, the Platform:
  * returns the error code.&#x20;
* If the result is _Success_, the Platform:
  * changes a user's status to _Paid_,
  * changes the user's traffic limit to _Unlimited,_
  * sends a _purchase\_id_ to the App_._

**Step 4.**  The Platform will check the _Purchase receipt_ every 24 hours.

* If the result is _Success_, the Platform:
  * does nothing.
* If the result is _Failed_, the Platform: &#x20;
  * changes the user's status to _Free_ ,
  * changes the user's bandwidth limit to _Free limit = 100Mb._

## Purchase receipt example

Purchase receipt should be in JSON format and include the following details:

| Field name        | Type         | Description                                                                                    |
| ----------------- | ------------ | ---------------------------------------------------------------------------------------------- |
| purchase\_info    | object       | Purchase vendor-specific data about the purchase, such as receipt                              |
| receipt           | object       | Raw JSON receipt of the purchase. “orderId” will be used as a unique key for each subscription |
| active\_timestamp | Number, Long | Active time for current subscription period                                                    |

body format

```
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

Detailed purchase info in the “_receipt"_

| Field name           | Type   | Description                                                                                                                                                                                     |
| -------------------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| orderId              | string | Unique identifier of the subscription which should not change upon renewal. This ID is used to verify purchase.                                                                                 |
| transactionId        | string | Unique identifier for each transaction (purchase), the payment system sends different IDs for different transactions.                                                                           |
| purchaseTime         | long   | Unix timestamp of the most recent subscription purchase                                                                                                                                         |
| expireTime           | long   | Unix timestamp of when the subscription is to expire                                                                                                                                            |
| purchaseState        | int    | <p><em>0</em>: Successful paid transaction, <em>1</em>: Refunded transaction, <em>2</em>: Free transaction (trial)</p><p>If it’s <em>null</em>, assume it is a successful paid transaction.</p> |
| trialLength          | int    | Number of days of free trial. _0_: No trial                                                                                                                                                     |
| usdAmount            | float  | Price of the subscription in USD. It is not mandatory, but it is desirable to have this in your project. If the user is on trial period, the value should be _0_.                               |
| originalPurchaseTime | long   | UNIX timestamp of when the first transaction was performed (the first purchase or trial start)                                                                                                  |
| planName             | string | Plan or SKU name of the subscription for reference                                                                                                                                              |
| type                 | string | Payment Plugin name                                                                                                                                                                             |

## Server side: Delete purchase

To delete a purchase, you need to call the API method DELETE [`/partner/subscribers/{user_id}/purchase`](https://backend.northghost.com/doc/all/index.html#!/partner-controller/deletePurchaseByPartner)with the following parameters:

| Field name     | Type    | Mandatory | Description                                                                                                                                                    |
| -------------- | ------- | --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| user\_id       | integer | Yes       | Unique user ID on the Platform                                                                                                                                 |
| access\_token  | string  | Yes       | Unique token for partner API. Expires every 24 hours.                                                                                                          |
| purchase\_id   | integer | Yes       | Platform purchase ID of the user. Sent back as a response when a purchase is added to a user.                                                                  |
| purchase\_info | object  | No        | Add the latest _purchase\_info_ to a purchase that is going to be deleted. It is important to change the _purchaseState_ appropriately, especially for refund. |

## Purchase receipt verification

Platform will call this POST method to verify a purchase (see **Steps 3-4** in the Flow diagram) when it is first performed, and every day after that.

**Parameters**

| Field name        | Type   | Description                                                                     | Mandatory |
| ----------------- | ------ | ------------------------------------------------------------------------------- | --------- |
| partner\_user\_id | string | Unique user id generated by the partner system                                  | Yes       |
| purchase\_info    | string | “orderId” must be present and is used as unique identifier for the verification | Yes       |

**Response**

| Field name | Type    | Description                                                                  | Mandatory |
| ---------- | ------- | ---------------------------------------------------------------------------- | --------- |
| is\_valid  | Boolean | A marker whether the purchase is valid or not. Possible values: _true/false_ | Yes       |
| user\_info | Object  | Details of current user parameters                                           | No        |
