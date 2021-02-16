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

# Addresses

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

# Cart

| Property     | Type   | Description                                   |
| ------------ | ------ | --------------------------------------------- |
| name         | string | Name of item                                  |
| price        | number | \* Price of item                              |
| sku          | string | Unique id of product                          |
| quantity     | number | Number of cart item purchased                 |
| variantId    | string | Id of cart Item Variant                       |
| productImage | string | URL pointing to product image                 |
| attributes   | map    | Arbitrary product attributes, e.g color, size |

# Orders

| Property            | Type    | Description                                                            |
| ------------------- | ------- | ---------------------------------------------------------------------- |
| orderId             | string  | Unique identification for an order                                     |
| name                | string  | Customer name                                                          |
| email               | string  | Customer's email                                                       |
| status              | string  | Order status; one of the following: `created`, `fulfilled`, `canceled` |
| address             | map     | ADDRESS                                                                |
| currency            | string  | Currency order was created in                                          |
| tax                 | number  | \* Tax paid on order                                                   |
| dutiesAndImportFees | number  | \* Duties and/or import fees                                           |
| shipping            | number  | \* Amount charged for shipping                                         |
| courier             | string  | Courier providing shipping quotes                                      |
| totalValue          | number  | \* Total amount paid, shipping and tax included                        |
| productCount        | number  | Total items purchased                                                  |
| cart                | array   | CART                                                                   |
| reorder             | boolean | `true` indicates a repeat order                                        |
| weight              | number  | Total weight of items in `KG`                                          |
| tracking_url        | string  | URL for tracking fulfilled orders                                      |
| downloadURL         | string  | URL for fulfilling downloadable orders                                 |
| isInternational     | string  | `true` indicates that the customer is in the same country              |

\* Prices are in fractional currency e.g cents.

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
			"courier": "USPS - Priority Mail",
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
curl "https://api.dola.me/api/orders/<orderID>"
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
		"courier": "USPS - Priority Mail",
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
		"tracking_url": "https://tracking-service.net/ksjdogiei32234kred",
		"isInternational": false
	}
}
```

This returns a single order given the order id is provided in the URL.

**HTTP Request**

`GET https://api.dola.me/api/orders/<orderID>`

**URL Parameters**

| Parameter | Optional | Description         |
| --------- | -------- | ------------------- |
| orderID   | false    | The id of the order |

## Update Order

> For physical products, The update endpoint can be used like this:

```shell
curl https://api.dola.me/api/orders/<orderID>
-X PATCH
-H "Content-Type: application/json"
-H "Accept: application/json"
-H "DOLA-API-KEY: dolaapikey"
-d "{\"tracking_url\": \"https://tracking-service.net/ksjdogiei32234kred\"}"
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
		"courier": "USPS - Priority Mail",
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
		"tracking_url": "https://tracking-service.net/ksjdogiei32234kred",
		"isInternational": false
	}
}
```

> For downloadable products, The update endpoint can be used like this:

```shell
curl https://api.dola.me/api/orders/<orderID>
-X PATCH
-H "Content-Type: application/json"
-H "Accept: application/json"
-H "DOLA-API-KEY: dolaapikey"
-d "{\"status\": \"fulfilled\", \"cart\": {\"downloadURL\":\"https://tracking-service.net/ksjdogiei32234kred\", \"sku\": \"dola-unicorn-hoodie-6\"}, }"
```

> This returns a JSON response with this structure: The difference being that the downloadURL is included in the cart response.

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
		"courier": "USPS - Priority Mail",
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
		"tracking_url": "https://tracking-service.net/ksjdogiei32234kred",
		"isInternational": false
	}
}
```

This marks an order as fulfilled, given the tracking url is in the request body.

**HTTP Request**

`PATCH https://api.dola.me/api/orders/<orderID>`

**Body Parameters**

**CART UPDATE**

| Parameter   | Optional | Description                                 |
| ----------- | -------- | ------------------------------------------- |
| downloadURL | false    | download url for downloadable product       |
| sku         | false    | Stock keeping unit for downloadable product |

| Parameter    | Optional | Description                                                            |
| ------------ | -------- | ---------------------------------------------------------------------- |
| tracking_url | true     | Tracking url for physical products                                     |
| status       | true     | Order status; one of the following: `created`, `fulfilled`, `canceled` |
| cart         | true     | CART UPDATE                                                            |

## Delete Order

```shell
curl https://api.dola.me/api/orders/<orderID>
-X DELETE
-H "Content-Type: application/json"
-H "Accept: application/json"
-H "DOLA-API-KEY: dolaapikey"
```

> This endpoint has no response body.

This cancels and refunds an order.

**HTTP Request**

`DELETE https://api.dola.me/api/orders/<orderID>`

**URL Parameters**

| Parameter | Optional | Description         |
| --------- | -------- | ------------------- |
| orderID   | false    | The id of the order |

# Errors

Dola's API uses the following error codes:

| Error Code | Meaning                                                                    |
| ---------- | -------------------------------------------------------------------------- |
| 401        | Unauthorized – Your API key is wrong.                                      |
| 403        | Forbidden – The requested resource is hidden for administrators only.      |
| 404        | Not Found – The specified resource could not be found.                     |
| 500        | Internal Server Error – We had a problem with our server. Try again later. |
