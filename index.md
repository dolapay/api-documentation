---
title: Dola API Documentation

language_tabs: # must be one of https://prismjs.com/#supported-languages
  - javascript

toc_footers:

favicon _tag: favicon.ico

includes:

search: false
code_clipboard: true
---

# Overview

This is Dola's API documentation; furthermore, our developer portal will be released in March (2021).

The Dola API is organized around [REST](http://en.wikipedia.org/wiki/Representational_State_Transfer). Our API has predictable resource-oriented URLs, accepts and returns [JSON](http://www.json.org/), and uses standard HTTP response codes, authentication, and verbs.

# Authorization

The Dola API uses API keys to authenticate requests. You can view and manage your API keys in your Dola Wallet. Note, only accounts with an approved Merchant Application are provided API keys. To submit a Merchant Application, go Settings in your Dola Wallet and click Apply.

Your API keys carry many privileges, so be sure to keep them secure! Do not share your secret API keys in publicly accessible areas such as GitHub, client-side code, and so forth.

Each API key has the following prefix: `dola_pay_`.

Provide your API Key in the following header:

> To authorize, use this code:

```javascript
`DOLA-API-KEY: {Your dola API Key}`;
```

> `DOLA-API-KEY: {Your dola API Key}`.

<aside class="notice">
You must replace <code>DOLA-API-KEY</code> with your Dola API key.
</aside>

# Orders

### Schema

#### CART

| Property     | type   | Description                                   |
| ------------ | ------ | --------------------------------------------- |
| name         | string | Name of item                                  |
| price        | number | \* Price of item                              |
| sku          | string | Unique id of product                          |
| quantity     | number | Number of cart item purchased                 |
| variantId    | string | Id of cart Item Variant                       |
| productImage | string | URL pointing to product image                 |
| attributes   | map    | Arbitrary product attributes, e.g color, size |

#### ADDRESS

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

#### ORDER

| Property            | type    | Description                                                            |
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
| productCount        | number  | \* Total items purchased                                               |
| cart                | array   | CART                                                                   |
| reorder             | boolean | `true` indicates a repeat order                                        |
| weight              | number  | \* Total weight of items in `KG`                                       |
| tracking_url        | string  | URL for tracking fulfilled orders                                      |
| isInternational     | string  | `true` indicates that the customer is in the same country              |

\* Prices are in fractional currency e.g cents.

### Endpoints:

- [Get All Orders](#get-all-orders)
- [Get Order](#get-order)
- [Update Order](#update-order)
- [Delete Order](#delete-order)

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

# Integrations

## Backendless Ecommerce Platform

### Overview

BEP is short for “Backendless Ecommerce Platform,” and it turns any website into a shop with just one line of code.

The best part?

BEP doesn't require a backend or CMS! Just add our snippet and you're in business _- literally!_

With BEP, you can instantly accept payments from 195 countries, ship globally, get paid, and it's free _- standard 2.9% + $0.30 processing fees apply._

Whether you're building a direct-to-consumer site, a landing page for your latest drop, or a side hustle with friends and family, BEP does it all.

Also, as orders come in, BEP provides you with everything you need to fulfill, including pre-paid duties, shipping, taxes, and more. BEP also comes with an API, accessible via API keys and a Zapier app, enabling you to build automations and sync data that's relevant to your business.

For now, BEP is available for merchants in the U.S. and U.K.; but, consumers everywhere can purchase from a BEP store.

To get started, reference the documentation below to add BEP to any static site.

[Demo Site](https://bep-example.dola.me/)

### Getting Started

1. Login to [Dola](https://dola.me).

2. Navigate to settings and click on `Become a merchant` and go through the onboarding process. Make sure that the `Website URL` field matches your website.

3. When setting up, depending on your use case, you can select the `Basic Installation` or `Javascript SDK` option. Paste the copied snippet in the `<head>` section of your base html file.

### Setup

### Basic Installation

There are 3 HTML data attributes that trigger actions. Each action attribute is used alongside other attributes that describe the product/cart details.

#### `data-dola-buynow`

When set to `"true"`, the element, when clicked, will trigger a checkout with the product information on that element.

```html
<div>
	<button
		data-dola-buynow="true"
		data-dola-quantity="1"
		data-dola-title="productName"
		data-dola-image="imageURL"
		data-dola-price="35000"
		data-dola-weight="3000"
		data-dola-sku="productsku"
		data-dola-id="uniqueProductId"
		data-dola-currency="USD"
		class="dola-dola-bills-yall"
	>
		Buy Now
	</button>
</div>
```

#### `data-dola-cart`

When set to `"true"`, this indicates that the product (represented by the other data attributes on that element) has been added to a shopping cart.

```html
<div
	class="dola-dola-bills-yall"
	data-dola-title="currentProductTitle"
	data-dola-title="productName"
	data-dola-image="imageURL"
	data-dola-price="35000"
	data-dola-weight="3000"
	data-dola-sku="productsku"
	data-dola-id="uniqueProductId"
	data-dola-currency="USD"
	data-dola-cart="true"
	data-dola-quantity="2"
>
	Checkout
</div>
```

#### `data-dola-cartaction`

When set to `"true"`, the element, when clicked, will trigger a checkout with all products that have been added to the cart (by having their `data-dola-cart` attribute set to `"true"`).

```html
<div>
	<button data-dola-currency="USD" data-dola-cartaction="true" class="dola-dola-bills-yall">
		Checkout
	</button>
</div>
```

Only 1 action type should be used on an element at a given time.

While BEP is loading, `dola-bep-loading` is added as a class to actionable HTML elements. This can be leveraged to implement styles and other behavior for the loading state.

### JavaScript SDK

Here's a basic example:

```js
const cart = {
	currency: "USD",
	items: [
		{
			id: "randomId",
			image: "https://linkToproductimage",
			quantity: 1,
			title: "sample product",
			price: 35000,
			grams: 543,
			sku: "randomproductsku",
			subTotal: 35000,
		},
	],
};

window.Dolapay.attachDola(cart, cb);
```

The `attachDola` method triggers an instance of Dola's 1-click Checkout. It accepts a cart object and a callback which fires in the case of a successful execution. Note, errors are handled by Dola.

### Reference

### Basic Installation

These are the custom data attributes supported by BEP, these attributes are used to describe product/cart details depending on the attached action attribute.

| Attribute             | Description                                                                                          |
| --------------------- | ---------------------------------------------------------------------------------------------------- |
| `data-dola-title`     | Required. It captures the name of the product.                                                       |
| `data-dola-quantity`  | Required. It captures the quantity of the product being purchased.                                   |
| `data-dola-image`     | Required. It refers to a the image for the product. It accepts a url string.                         |
| `data-dola-price`     | Required. It captures the price of the product.                                                      |
| `data-dola-weight`    | Required. It captures the weight of the product. Adjust for the quantity of product being purchased. |
| `data-dola-id`        | Required. It refers to the unique id of this product.                                                |
| `data-dola-sku`       | Required. It refers to your sku for the product.                                                     |
| `data-dola-currency`  | Required. It sets the currency you want payments in.                                                 |
| `data-dola-variant-*` | Optional. It is used to set variants, where `*` is replaced by the name of the variant.              |

There is support for `Simple` and `Complex` type products.

- `Simple`: This is a product that has no variants. Below is an example of a simple product.

```html
<div>
	<button
		class="window.Dolapay.id"
		data-dola-buynow="true"
		data-dola-quantity="1"
		data-dola-title="productName"
		data-dola-image="imageURL"
		data-dola-price="35000"
		data-dola-weight="3000"
		data-dola-sku="productsku"
		data-dola-id="uniqueProductId"
		data-dola-currency="USD"
	>
		Buy Now
	</button>
</div>
```

- `Complex`: This refers to a product that has variants. Custom variants can be added with the `data-dola-variant-*` attribute. Below is an example of a complex product.

```html
<div>
	<button
		data-dola-buynow="true"
		data-dola-quantity="1"
		data-dola-title="productName"
		data-dola-image="imageURL"
		data-dola-price="35000"
		data-dola-weight="3000"
		data-dola-sku="productsku"
		data-dola-id="uniqueProductId"
		data-dola-currency="USD"
		data-dola-variant-color="red"
		class="window.Dolapay.id"
	>
		Buy Now
	</button>
</div>
```

### JavaScript SDK

The script snippet initialises Dola and attaches a global `Dolapay` object to the global `Window` object. The global Dolapay object can be accessed via `window.Dolapay`.

```ts
interface IDolapay {
  id: string;
  attachDola?: (cart: Cart, callback: () => void) => void;
  type?: string;
  orderCompleted: boolean;
}


window.Dolapay:IDolapay
```

- `type`: This property refers to the initialization method of the BEP instance.

  - `basic`: means the BEP instance was created as a `JavaScript SDK` instance.
  - `custom`: means the BEP instance was created as an `Basic Installation` instance.

- `orderCompleted`: This property exposes the state of the current order.

- `id`: This property refers to your `merchantId` it is included in the script snippet copied from the developers section of your profile settings.

- `attachDola`: This method triggers an instance of Dola's 1-click Checkout. It accepts a `Cart` object and a callback which fires in the case of a successful execution. Errors are visually handled by Dola's 1-click Checkout.

```ts
interface Cart {
	currency: string;
	items: CartItem[];
}

interface CartItem {
	id: string;
	image: string;
	quantity: number;
	title: string;
	price: number;
	grams: number;
	variantInfo?: VariantInfo[];
	sku?: string;
	subTotal: number;
}

interface VariantInfo {
	id: string;
	name: string;
	value: string;
}
```

### Browser Compatibility

- last 2 Chrome versions
- last 2 Firefox versions
- last 2 Edge versions
- modern browsers

## Shopify

This is Dola's Shopify store integration. This script is responsible for handling Dola's integration with Shopify stores.

### Onboarding

Before proceeding to integrating the button, please make sure you have successfully completed the Dola merchant onboarding process on our website and that you've been provided with a `merchantID`. This will be used in the integration below.

1. Paste a copy of this script in the `theme.liquid` file in the layout section of the shopify
   theme, paste the button at the bottom of the `<body></body>` section.

```html
<script id="doladolabillsyall" defer data-dola-merchant-id="yourMerchantID">
	var script = document.createElement("script");

	script.src = "https://dola-shopify-script.vercel.app/index.js";
	script.async = true;

	var entry = document.getElementsByTagName("script")[0];
	entry.parentNode.insertBefore(script, entry);
</script>
```

2. The Shopify script, exposes 4 classes to trigger Dola's checkout integration on different parts of your shopify store.

   - `dola-dola-bills-yall-instant`: Attached to single products, will only display and trigger checkout when cart is empty.

   - `dola-dola-bills-yall-cart`: Attached to cart modal, this allows Dola bind with a trigger event to the cart modal.

   - `dola-dola-bills-yall-checkout`: This is used along with `dola-dola-bills-yall-cart`. It is attached to the point in the cart modal, where the Dola Checkout button should be displayed.

   - `dola-dola-bills-yall`: Attached to cart page, this triggers Dola checkout.

## Zapier

In order to automate post-purchase activities such as customer support, fulfillment, marketing, and more, we've integrated Dola with Zapier.

> To get started with setting up this integration, all you'll require is a [Zapier account](https://zapier.com/).

After setting up your account, navigate to [Dola's Zapier Integration page](https://zapier.com/apps/dola/integrations). Here, you can select from Dola's existing workflows or choose to build a custom workflow zap for yourself.

Dola's Zapier integration includes:

### Triggers

`New Order`: This trigger fires when a new order has been created for the merchant. It returns details about newly created order that are necessary to create fulfilment details.

### Actions

`Update Order`: This is an action that is fired to update a specific order's details.
