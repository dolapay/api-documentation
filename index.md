---
title: Dola API Documentation

language_tabs: # must be one of https://prismjs.com/#supported-languages
  - shell

toc_footers:

favicon _tag: favicon.ico

includes:

search: false
code_clipboard: true
---

# Overview

The Dola API is organized around [REST](http://en.wikipedia.org/wiki/Representational_State_Transfer). Our API has predictable resource-oriented URLs, accepts and returns [JSON](http://www.json.org/), and uses standard HTTP response codes, authentication, and verbs.

# Authorization

> To authorize, use this code:

```shell
curl "api_endpoint_here"
-H "DOLA-API-KEY: dolaapikey"
```

> Make sure to replace `dolaapikey` with your API key.
> The Dola API uses API keys to authenticate requests. You can view and manage your API keys in your Dola Wallet.

Your API keys carry many privileges, so be sure to keep them secure! Do not share your secret API keys in publicly accessible areas such as GitHub, client-side code, and so forth. Each API key has the following prefix: `dola_pay_`.

Dola expects for the API key to be included in all API requests to the server in a header that looks like the following:

# Schema

## Address

| Property      | Type    | Description                                 |
| ------------- | ------- | ------------------------------------------- |
| address1      | string  | Street address                              |
| address2      | string  | Optional additional street address          |
| city          | string  | City or Town                                |
| state         | string  | State or Province                           |
| country       | string  | Country                                     |
| zipCode       | string  | Zip/postal code                             |
| insured       | boolean | `true` indicates insurance for this address |
| lastName      | string  | Last name registered on address             |
| firstName     | string  | First name registered on address            |
| isResidential | boolean | `true` indicates a residential address      |

## Cart

| Property     | Type   | Description                                   |
| ------------ | ------ | --------------------------------------------- |
| name         | string | Name of item                                  |
| price        | number | \* Price of item                              |
| sku          | string | Unique id of product                          |
| quantity     | number | Number of cart item purchased                 |
| variantId    | string | Id of cart Item Variant                       |
| productImage | string | URL pointing to product image                 |
| attributes   | map    | Arbitrary product attributes, e.g color, size |

## Tracking

| Property    | Type   | Description                       |
| ----------- | ------ | --------------------------------- |
| trackingId  | string | Fulfilment Id provided by courier |
| trackingURL | string | URL required to track fulfilment  |
| courier     | string | Courier                           |
| id          | string | Fulfilment Id provided by Dola    |

## Order

| Property                  | Type    | Description                                                                      |
| ------------------------- | ------- | -------------------------------------------------------------------------------- |
| orderId                   | string  | Unique identification for an order                                               |
| name                      | string  | Customer name                                                                    |
| email                     | string  | Customer's email                                                                 |
| status                    | string  | Order status; one of the following: `created`, `fulfilled`, `canceled`           |
| address                   | map     | ADDRESS                                                                          |
| currency                  | string  | Currency order was created in                                                    |
| tax                       | number  | \* Tax paid on order                                                             |
| dutiesAndImportFees       | number  | \* Duties and/or import fees                                                     |
| shipping                  | number  | \* Amount charged for shipping                                                   |
| totalValue                | number  | \* Total amount paid, shipping and tax included                                  |
| productCount              | number  | Total items purchased                                                            |
| cart                      | array   | CART                                                                             |
| reorder                   | boolean | `true` indicates a repeat order                                                  |
| weight                    | number  | Total weight of items in `KG`                                                    |
| trackingInfo              | array   | TRACKING                                                                         |
| downloadURL               | string  | URL for fulfilling downloadable orders                                           |
| isInternational           | boolean | `true` indicates that the customer is in the same country                        |
| containsNonShippableItems | boolean | `true` indicates that the product is not a physical product and can't be shipped |

\* Prices are in fractional currency e.g cents.

# API
## Get All Orders

```shell
curl "https://api.dola.me/api/orders"
-H "Content-Type: application/json"
-H "Accept: application/json"
-H "DOLA-API-KEY: dolaapikey"
```

> This returns a JSON response with this structure:

```json
{
  "message": "Success",
  "data": [
    {
      "orderId": "I7nt5K7jaUp06vn78UOC",
      "name": "Linus Turaki",
      "email": "chubi+99@dola.me",
      "status": "created",
      "address": {
        "address1": "607 Pine Oaks Dr",
        "city": "Tunnel Hill",
        "state": "GA",
        "country": "US",
        "zipCode": "30755",
        "insured": true,
        "lastName": "Turaki",
        "firstName": "Linus",
        "isResidential": true
      },
      "currency": "USD",
      "tax": 996,
      "dutiesAndImportFees": 0,
      "shipping": 767,
      "trackingInfo": [
        {
          "id": "HSAPqHOLPJWLkiGMRuxK",
          "trackingURL": "https://tracking-service.net/ksjdogiei32234kred"
        },
        {
          "id": "PAkrEXgDwayoecUHSbRb",
          "courier": "UPSS",
          "trackingURL": "https://tracking-service.net/ksjdogiei32234kred",
          "trackingId": "i3mdaj3i"
        }
      ],
      "totalValue": 11762,
      "productCount": 1,
      "cart": [
        {
          "name": "Hoodie (D)",
          "price": 9999,
          "sku": "dola-unicorn-hoodie-6",
          "quantity": 1,
          "variantId": "36493469483164",
          "productImage": "https://cdn.shopify.com/s/files/1/0481/1459/8044/products/dola-sample-product.jpg?v=1602787922",
          "attributes": {
            "exists": true
          }
        }
      ],
      "reorder": true,
      "weight": 0.45,
      "isInternational": false
    }
  ]
}
```

This returns all your orders.

**HTTP Request**

`GET https://api.dola.me/api/orders`

## Get Order

```shell
curl "https://api.dola.me/api/orders/<orderId>"
-H "Content-Type: application/json"
-H "Accept: application/json"
-H "DOLA-API-KEY: dolaapikey"
```

> This returns a JSON response with this structure:

```json
{
  "message": "Success",
  "data": {
    "orderId": "CvJSHoAqcQnPppggHBi8",
    "name": "Omoefe Dukuye",
    "email": "omoefe@dola.me",
    "status": "canceled",
    "address": {
      "address1": "166 2nd Ave N",
      "address2": "",
      "city": "Nashville",
      "state": "TN",
      "country": "US",
      "zipCode": "37201",
      "insured": false,
      "lastName": "Dukuye",
      "firstName": "Omoefe",
      "isResidential": true
    },
    "currency": "USD",
    "tax": 996.7,
    "dutiesAndImportFees": 100,
    "shipping": 767,
    "trackingInfo": [
      {
        "id": "HSAPqHOLPJWLkiGMRuxK",
        "trackingURL": "https://tracking-service.net/ksjdogiei32234kred"
      },
      {
        "id": "PAkrEXgDwayoecUHSbRb",
        "courier": "UPSS",
        "trackingURL": "https://tracking-service.net/ksjdogiei32234kred",
        "trackingId": "i3mdaj3i"
      }
    ],
    "totalValue": 11762,
    "productCount": 1,
    "cart": [
      {
        "name": "Hoodie (D)",
        "price": 9999,
        "sku": "dola-unicorn-hoodie-6",
        "quantity": 1,
        "variantId": "3649369483164",
        "productImage": "https://cdn.shopify.com/s/files/1/0481/1459/8044/products/dola-sample-product.jpg?v=1602787922",
        "attributes": {
          "exists": true
        }
      }
    ],
    "reorder": false,
    "weight": 0.45,
    "isInternational": false
  }
}
```

This returns a single order given the order id is provided in the URL.

**HTTP Request**

`GET https://api.dola.me/api/orders/<orderId>`

**URL Parameters**

| Parameter | Optional | Description         |
| --------- | -------- | ------------------- |
| orderId   | false    | The id of the order |

## Update Order

> For physical products, The update endpoint can be used like this:

```shell
curl https://api.dola.me/api/orders/<orderId>
-X PATCH
-H "Content-Type: application/json"
-H "Accept: application/json"
-H "DOLA-API-KEY: dolaapikey"
-d "{\"fulfill\":false,\"attachments\":{\"linkToInstructions\":\"https:\/\/product-usage-instructions.net\/ksjdogiei32234kred\"},\"originAddress\":{\"city\":\"bogota\"}}"
```

> This returns a JSON response with this structure:

```json
{
  "message": "Success",
  "data": {
    "orderId": "CvJSHoAqcQnPppggHBi8",
    "name": "Omoefe Dukuye",
    "email": "omoefe@dola.me",
    "status": "created",
    "address": {
      "address1": "166 2nd Ave N",
      "address2": "",
      "city": "Bogota",
      "state": "TN",
      "country": "US",
      "zipCode": "37201",
      "insured": false,
      "lastName": "Dukuye",
      "firstName": "Omoefe",
      "isResidential": true
    },
	"attachments": {
      "linkToInstructions": "https://product-usage-instructions.net/ksjdogiei32234kred"
    },
    "currency": "USD",
    "tax": 996.7,
    "dutiesAndImportFees": 100,
    "shipping": 767,
    "trackingInfo": [
      {
		"id": "PAkrEXgDwayoecUHSbRb",
        "courier": "DHL",
		"trackingURL": "https://tracking-service.net/ksjdogiei32234kred",
        "trackingId": "aaDAksddikdD"
      }
    ],
    "totalValue": 11762,
    "productCount": 1,
    "cart": [
      {
        "name": "Hoodie (D)",
        "price": 9999,
        "sku": "dola-unicorn-hoodie-6",
        "quantity": 1,
        "variantId": "3649369483164",
        "productImage": "https://cdn.shopify.com/s/files/1/0481/1459/8044/products/dola-sample-product.jpg?v=1602787922",
        "attributes": {
          "exists": true
        }
      }
    ],
    "reorder": false,
    "weight": 0.45,
    "isInternational": false
  }
}
```

> For non-shippable products, The update endpoint can be used like this:

```shell
curl https://api.dola.me/api/orders/<orderId>
-X PATCH
-H "Content-Type: application/json"
-H "Accept: application/json"
-H "DOLA-API-KEY: dolaapikey"
-d "{\"fulfill\": true, \"attachments\": {\"downloadURL\":\"https:\/\/dowload-site.net\/ksjdogiei32234kred\"}}"
```

> This returns a JSON response with this structure.

```json
{
  "message": "Success",
  "data": {
    "orderId": "CvJSHoAqcQnPppggHBi8",
    "name": "Omoefe Dukuye",
    "email": "omoefe@dola.me",
    "status": "fulfilled",
    "address": {
      "address1": "166 2nd Ave N",
      "address2": "",
      "city": "Nashville",
      "state": "TN",
      "country": "US",
      "zipCode": "37201",
      "insured": false,
      "lastName": "Dukuye",
      "firstName": "Omoefe",
      "isResidential": true
    },
	"attachments": {
      "downloadURL": "https://dowload-site.net/ksjdogiei32234kred"
    },
    "currency": "USD",
    "tax": 996.7,
    "dutiesAndImportFees": 100,
    "shipping": 767,
    "trackingInfo": [
      {
        "id": "HSAPqHOLPJWLkiGMRuxK",
        "trackingURL": "URL.TRACKY"
      },
      {
        "id": "PAkrEXgDwayoecUHSbRb",
        "courier": "UPSS",
        "trackingURL": "URL.TRACKI",
        "trackingId": "i3mdaj3i"
      }
    ],
    "totalValue": 11762,
    "productCount": 1,
    "cart": [
      {
        "name": "Hoodie (D)",
        "price": 9999,
        "sku": "dola-unicorn-hoodie-6",
        "quantity": 1,
        "variantId": "3649369483164",
        "productImage": "https://cdn.shopify.com/s/files/1/0481/1459/8044/products/dola-sample-product.jpg?v=1602787922",
        "downloadURL": "https://downloadURL-service-cdn/kf5ge234kred",
        "attributes": {
          "exists": true
        }
      }
    ],
    "reorder": false,
    "weight": 0.45,
    "isInternational": false
  }
}
```

This marks an order as fulfilled, given the tracking url is in the request body.

**HTTP Request**

`PATCH https://api.dola.me/api/orders/<orderId>`

**Body Parameters**

| Parameter    | Optional | Description                                                            |
| ------------ | -------- | ---------------------------------------------------------------------- |
| fulfill | false     | Marks an order as fulfilled and completes the transaction                  |
| attachments     | true     | Arbitrary properties added to an object |
| originAddress         | true     |  Updates the origin address on an order                       |

## Delete Order

```shell
curl https://api.dola.me/api/orders/<orderId>
-X DELETE
-H "Content-Type: application/json"
-H "Accept: application/json"
-H "DOLA-API-KEY: dolaapikey"
```

> This endpoint has no response body.

This cancels and refunds an order.

**HTTP Request**

`DELETE https://api.dola.me/api/orders/<orderId>`

**URL Parameters**

| Parameter | Optional | Description         |
| --------- | -------- | ------------------- |
| orderId   | false    | The id of the order |

## Add Tracking

```shell
curl https://api.dola.me/api/orders/<orderId>/trackingInfo
-X POST
-H "Content-Type: application/json"
-H "Accept: application/json"
-H "DOLA-API-KEY: dolaapikey"
-d "{\"trackingURL\":\"https:\/\/tracking-service.net\/ksjdogiei32234kred\",\"courier\":\"DHL\",\"trackingId\":\"aaDAksddikdD\"}"
```

> This endpoint has no response body.

This adds fulfilment and tracking info to an order(supports multiple partial fulfilments).

**HTTP Request**

`POST https://api.dola.me/api/orders/<orderId>/trackingInfo`

**URL Parameters**

| Parameter | Optional | Description         |
| --------- | -------- | ------------------- |
| orderId   | false    | The id of the order |

**Body Parameters**

| Parameter    | Optional | Description                                                            |
| ------------ | -------- | ---------------------------------------------------------------------- |
| trackingId | true     | Fulfilment Id provided by courier                |
| trackingURL | false     | URL required to track fulfilment |
| courier    | true     |  Courier fulfilling order  |

## Delete Tracking

```shell
curl https://api.dola.me/api/orders/<orderId>/trackingInfo/<Id>
-X Delete
-H "Content-Type: application/json"
-H "Accept: application/json"
-H "DOLA-API-KEY: dolaapikey"
```

> This endpoint has no response body.

This removes fulfilment and tracking info from an order.

**HTTP Request**

`DELETE https://api.dola.me/api/orders/<orderId>/trackingInfo/<Id>`

**URL Parameters**

| Parameter | Optional | Description                   |
| --------- | -------- | ----------------------------- |
| orderId   | false    | The id of the order           |
| Id        | false    | The id of the tracking object |

# Errors

Dola's API uses the following error codes:

| Error Code | Meaning                                                                    |
| ---------- | -------------------------------------------------------------------------- |
| 401        | Unauthorized – Your API key is wrong.                                      |
| 403        | Forbidden – The requested resource is hidden for administrators only.      |
| 404        | Not Found – The specified resource could not be found.                     |
| 500        | Internal Server Error – We had a problem with our server. Try again later. |
