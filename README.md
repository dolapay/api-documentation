# Dola's API Documentation
This is Dola's temporary API documentation; furthermore, our developer portal will be released in March (2021).

## Basics

### API Reference

The Dola API is organized around [REST](http://en.wikipedia.org/wiki/Representational_State_Transfer). Our API has predictable resource-oriented URLs, accepts [form-encoded](https://en.wikipedia.org/wiki/POST_(HTTP)#Use_for_submitting_web_forms) request bodies, returns [JSON-encoded](http://www.json.org/) responses, and uses standard HTTP response codes, authentication, and verbs.

:link: `Base URL: https://api.dola.me/api`
### Authorization

The Dola API uses API keys to authenticate requests. You can view and manage your API keys in your Dola Wallet. Note, only accounts with an approved Merchant Application are provided API keys. To submit a Merchant Application, go Settings in your Dola Wallet and click Apply.

Your API keys carry many privileges, so be sure to keep them secure! Do not share your secret API keys in publicly accessible areas such as GitHub, client-side code, and so forth.

Each API key has the following prefix: `dola_pay_`.

Provide your API Key in the following header:

:warning: `DOLA-API-KEY: {Your dola API Key}`

## Orders

Available endpoints:

* [Get All Orders](#get-all-orders)
* [Get Order](#get-order)
* [Update Order](#update-order)
* [Delete Order](#delete-order)

### Get All Orders

`GET /order`

This returns all your orders.

Sample response:

`Status: 200`

`Body:`

```json
{
  "message": "Success",
  "data": [
    {
      "id": "ID",
      "product": "Anything, something",
      "chargeId": "STRIPE_CHARGE_ID",
      "address": {
        "name": "Daniel James",
        "firstName": "Daniel",
        "address1": "333 Fremont St",
        "insured": false,
        "lastName": "James",
        "country": "US",
        "zipCode": "94105",
        "state": "CA",
        "id": "ID",
        "isResidential": true,
        "defaultAddress": true,
        "city": "SF"
      },
      "shopperId": "SHOPPER_ID",
      "currency": "NGN",
      "shipping": 334400.05544,
      "shopId": "SHOP_ID",
      "totalValue": 375820.06230700004,
      "weight": 0.3,
      "func": false,
      "shop": "javascript",
      "tax": 3420.000567,
      "name": "Daniel James",
      "orderId": "ORDER_ID",
      "cart": [
        {
          "sku": "anythingsomethingskku",
          "name": "Anything, something",
          "productImage": "imageURL",
          "quantity": 1,
          "price": 38000.0063,
          "attributes": {},
          "variantId": "1231"
        }
      ],
      "courier": "USPS - Priority Mail",
      "tracking_url": "URL.TRACK",
      "businessName": "Joygate Ventures",
      "productCount": 1,
      "isInternational": false,
      "email": "customer@email.com",
      "merchantId": "MERCHANT_ID",
      "status": "fulfilled",
      "customerSupportEmail": "customerSupport@company.com",
      "dutiesAndImportFees": 0
    }
  ]
}
```

### Get Order

`GET /order/{orderId}`

This returns a single order given the order id is provided in the URL.

Sample response:

`Status: 200`

`Body:`

```json
{
  "message": "Success",
  "data": {
    "status": "fulfilled",
    "isInternational": false,
    "dutiesAndImportFees": "0",
    "shopperId": "SHOPPER_ID",
    "currency": "NGN",
    "businessName": "Joygate Ventures",
    "productCount": "1",
    "shopId": "SHOP_ID",
    "chargeId": "STRIPE_CHARGE_ID",
    "created": 1612457520,
    "totalValue": 375820.06230700004,
    "merchantId": "YOUR_MERCHANT_ID",
    "address": {
      "zipCode": "94105",
      "insured": false,
      "lastName": "James",
      "name": "Daniel James",
      "updated": 1612032137,
      "state": "CA",
      "city": "SF",
      "country": "US",
      "id": "id",
      "created": 1608817978,
      "defaultAddress": true,
      "isResidential": true,
      "address1": "333 Fremont St",
      "firstName": "Daniel"
    },
    "tax": 3420.000567,
    "name": "Daniel James",
    "update": 1612457523,
    "courier": "USPS - Priority Mail",
    "shipping": 334400.05544,
    "customerSupportEmail": "customerSupport@company.com",
    "shop": "javascript",
    "orderId": "ORDER_ID",
    "tracking_url": "URL.TRACK",
    "cart": [
      {
        "name": "Anything, something",
        "price": 38000.0063,
        "sku": "anythingsomethingskku",
        "quantity": "1",
        "variantId": "1231",
        "attributes": {
        },
        "productImage": "imageURL"
      }
    ],
    "func": false,
    "product": "Anything, something",
    "email": "customer@email.com",
    "date": 1612457520,
    "weight": 0.3
  }
}
```

### Update Order

`PATCH /order/{orderId}`

This marks an order as fulfilled, given the tracking url is in the request body.

```json
{
    "tracking_url": "https://tracking-service.net/ksjdogiei32234kred"
}
```

Sample response:

`Status: 200`

### Delete Order

`DELETE /order/{orderId}`

This cancels and refunds an order.

Sample response:

`Status: 200`
