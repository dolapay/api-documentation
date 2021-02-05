# Dola API Documentation
Temporary home for Dola's API Documentation.

## Order API Specification
`Base URL: https://api.dola.me/api`
### Authorization

Provide your Dola API Key in the following header:

`DOLA-API-KEY: {Your dola API Key}`

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
        "created": {
          "_seconds": 1608817978,
          "_nanoseconds": 277000000
        },
        "address1": "333 Fremont St",
        "insured": false,
        "lastName": "James",
        "country": "US",
        "zipCode": "94105",
        "state": "CA",
        "id": "ID",
        "isResidential": true,
        "updated": {
          "_seconds": 1612032137,
          "_nanoseconds": 543000000
        },
        "defaultAddress": true,
        "city": "SF"
      },
      "update": {
        "_seconds": 1612457523,
        "_nanoseconds": 806000000
      },
      "shopperId": "SHOPPER_ID",
      "currency": "NGN",
      "shipping": 334400.05544,
      "shopId": "SHOP_ID",
      "totalValue": 375820.06230700004,
      "weight": 0.3,
      "created": {
        "_seconds": 1612457520,
        "_nanoseconds": 741000000
      },
      "func": false,
      "date": {
        "_seconds": 1612457520,
        "_nanoseconds": 741000000
      },
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

`GET /order/{order id}`

This returns a single order given the order id is provided in the URL.

Sample response:

`Status: 200`

`Body:`

```json
{
  "message": "Success",
  "data": {
    "exists": true,
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
      "exists": true,
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
        "exists": true,
        "name": "Anything, something",
        "price": 38000.0063,
        "sku": "anythingsomethingskku",
        "quantity": "1",
        "variantId": "1231",
        "attributes": {
          "exists": true
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
    tracking_url: https://tracking-service.net/ksjdogiei32234kred
}
```

Sample response:

`Status: 200`

### Delete Order

`DELETE /order/{orderId}`

This cancels and refunds an order.

Sample response:

`Status: 200`
