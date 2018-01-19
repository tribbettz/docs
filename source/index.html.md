---
title: Everlywell Enterprise API Reference

language_tabs:
  - http

search: true
---

# Introduction

Documentation for EverlyWell's Enterprise APIs.

# Auth API

## Issue Token

Authorize and Issue Token

```http
GET https://auth.everlywell.com/api/v1/token HTTP/1.1
Content-Type: application/json; charset=utf-8
Authorization: Basic <BASIC_AUTH_HERE>
```

> Response Definition

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

```json
{
  "token": "<JWT_TOKEN>"
}
```

###All Requests will be made in two parts

1. Acquire an access token from the Auth API
2. Use the access token as a bearer token for all other APIs

# Orders API

## Create Order

Create an Order.

> Request Definition

```http
POST https://secure.everlywell.com/aapi/v2/orders/ HTTP/1.1
Content-Type: application/json; charset=utf-8
Authorization: Bearer <JWT_TOKEN_HERE>
```

```json
{
  "email": "example@everlywell.com",
  "line_items": [
    {
      "product_id": 1,
      "quantity": 1
    }
  ],
  "ship_address": {
    "firstname": "Joe",
    "lastname":  "Example",
    "address1":  "800 W Cesar Chavez St",
    "address2":  "B101",
    "city":      "Austin",
    "state":     "TX",
    "zipcode":   "78701",
    "country":   "US",
    "phone":     "5125551234"
  }
}
```

### Query Parameters

Parameter | Required | Type | Description
--------- | ------- | ----------- | -------
email | true | string | User Email
line_items | true | array | Array of Line Items
product_id | true | int | Product ID for line item
quantity | true | int | Quantity for line item
ship_address | true | object | Address for shipment
firstname | true | string | First Name of recipient
lastname | true | string | Last Name of recipient
address1 | true | string | Address line 1
address2 | false | string | Address line 2
city | true | string | City
zipcode | true | string | Zipcode Format: 11111
phone | false | string | Phone number Format: (512) 555-1234 or 5125551234
state | true | string | State Format: TX
country | true | string | Country Format: US

> Response Definition

```http
HTTP/1.1 201 Created
Content-Type: application/json
```

```json
{
  "id": 50,
  "number": "R763740DD937E473E9AC911219E6805B",
  "email": "example@everlywell.com",
  "total": "0.0",
  "adjustment_total": "-99.0",
  "promo_total": "0.0",
  "state": "complete",
  "payment_state": "paid",
  "user_id": null,
  "bill_address_id": 69,
  "ship_address_id": 68,
  "item_count": 1,
  "channel": "spree"
}
```


# Results API

## Get Result

Get single Result by ID.


> Request Definition

```http
GET https://secure.everlywell.com/aapi/v1/results/<result_id> HTTP/1.1
Content-Type: application/json; charset=utf-8
Authorization: Bearer <JWT_TOKEN_HERE>
```

### Query Parameters

Parameter | Required | Type | Description
--------- | ------- | ----------- | -------
id | true | int | The result's ID


> Response Definition

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

```json
{
    "id": 1,
    "state": "ready",
}
```

