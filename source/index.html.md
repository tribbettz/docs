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

### Production URL
`GET https://auth.everlywell.com/api/v1/token`

### Staging URL
`GET https://auth-staging.everlywell.com/api/v1/token`

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


# Users API

## Create User

Create a User.

### Production URL
`POST https://secure.everlywell.com/ent/v1/users`

### Staging URL
`POST https://secure-staging.everlywell.com/ent/v1/users`

> Request Definition

```http
POST https://secure.everlywell.com/ent/v1/users/ HTTP/1.1
Content-Type: application/json; charset=utf-8
Authorization: Bearer <JWT_TOKEN_HERE>
```

```json
{
  "email": "example@everlywell.com",
  "firstname": "Joe",
  "lastname":  "Example",
  "dob": "2018-01-01",
  "gender": "male",
  "phone_number": "512-555-4564",
  "address": {
    "address1":  "800 W Cesar Chavez St",
    "address2":  "B101",
    "city":      "Austin",
    "state":     "TX",
    "zipcode":   78701,
    "country":   "US"
  }
}
```

### Query Parameters

Parameter | Required | Type | Description
--------- | ------- | ----------- | -------
email | true | string | User Email
firstname | true | string | First Name of the customer taking the test
lastname | true | string | Last Name of the customer taking the test
dob | true | string | Date of Birth in seconds for the User
gender | true | string | Gender of the User, Format: "male" or "female"
phone | false | int | Phone number Format: 5125551234
address | true | object | Address of the customer taking the test
address1 | true | string | Address line 1
address2 | false | string | Address line 2
city | true | string | City
zipcode | true | int | Zipcode Format: 11111
state | true | string | State Format: TX
country | true | string | Country Format: US

> Response Definition

```http
HTTP/1.1 201 Created
Content-Type: application/json
```

```json
{
  "id": "52354"
}
```


# Orders API

## Create Order

Create an Order.

### Production URL
`POST https://secure.everlywell.com/ent/v1/orders`

### Staging URL
`POST https://secure-staging.everlywell.com/ent/v1/orders`

> Request Definition

```http
POST https://secure.everlywell.com/ent/v1/orders/ HTTP/1.1
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
    "zipcode":   78701,
    "country":   "US",
    "phone":     5125551234
  },
  "auto_register": false,
  "user_id": 1
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
zipcode | true | int | Zipcode Format: 11111
phone | false | int | Phone number Format: 5125551234
state | true | string | State Format: TX
country | true | string | Country Format: US
auto_register | false | boolean | true will auto register the kit to the specified user_id
user_id | false | int | Optionally provide a user's id to associate the order

> Response Definition

```http
HTTP/1.1 201 Created
Content-Type: application/json
```

```json
{
  "number": "RB6E2BEA57E27456BA53D3A2D63125A5",
  "amount": "99.0",
  "email": "customer@email.com"
}
```


# Kits API

## Create Kit Registration

Create an Kit Registration for a User.

### Production URL
`POST https://secure.everlywell.com/ent/v1/kits/registration`

### Staging URL
`POST https://secure-staging.everlywell.com/ent/v1/kits/registration`

> Request Definition

```http
POST https://secure.everlywell.com/ent/v1/kits/registration HTTP/1.1
Content-Type: application/json; charset=utf-8
Authorization: Bearer <JWT_TOKEN_HERE>
```

```json
{
  "kit_id": "ABCDEF4567",
  "user": {
    "email": "test@email.com",
    "first_name": "Test",
    "last_name": "Testerson",
    "dob": 1476551410009,
    "phone_number": 5125557485,
    "gender": "male"
  },
  "address": {
    "address1": "123 Test str",
    "address2": "",
    "city": "Austin",
    "state": "TX",
    "zipcode": 78701
  }
}
```

### User

Parameter | Required | Type | Description
--------- | ------- | ----------- | -------
email | true | string | Email for the User associated with the Kit
first_name | true | string | First name of the User associated with the Kit
last_name | true | string | Last name of the User associated with the Kit
dob | true | int | Date of Birth in seconds for the User associated with the Kit
phone_number | true | int | Email associated with the Kit
gender | true | string | Gender of the User associated with the Kit Format: "male" or "female"

### Address

Parameter | Required | Type | Description
--------- | ------- | ----------- | -------
street1 | true | string | Street address associated with the User
street2 | False | string | Additional street address information associated with the User
city | true | string | City address associated with the User
state | true | string | State address associated with the User
zipcode | true | int | Zipcode address associated with the User



> Response Definition

```http
HTTP/1.1 201 Created
Content-Type: application/json
```

```json
{
    "id": 1,
    "state": "registred",
    "kit_id": "ABCDEF4567"
}
```


## Get Result

Get single Result by Kit ID for a registered Kit

### Production URL
`GET https://secure.everlywell.com/ent/v1/kits/<kit_id>`

### Staging URL
`GET https://secure.everlywell.com/ent/v1/kits/<kit_id>`

> Request Definition

```http
GET https://secure.everlywell.com/ent/v1/kits/<kit_id> HTTP/1.1
Content-Type: application/json; charset=utf-8
Authorization: Bearer <JWT_TOKEN_HERE>
```

### Query Parameters

Parameter | Required | Type | Description
--------- | ------- | ----------- | -------
kit_id | true | int | The result's ID


> Response Definition

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

```json
{
  "id": 1,
  "state": "ready",
  "name": "Breast Milk DHA",
  "markers": [
    {
      "id": 231,
      "units": "%",
      "descriptors": [
        "Low",
        "Normal"
        ],
      "boundaries": [
        0.32
      ]
    }
  ],
  "marker_results": [
    {
      "marker_id": 231,
      "value": 0.21,
    }
  ]
}
```


## List Kits 

Get a list of Kits matching the filter query params. 
(TEMPORARY ENDPOINT UNTIL EVENT WEBHOOKS)

### Production URL
`GET https://secure.everlywell.com/ent/v1/kits?<param1>=<value1>`

### Staging URL
`GET https://secure.everlywell.com/ent/v1/kits?<param1>=<value1>`

> Request Definition

```http
GET https://secure.everlywell.com/ent/v1/kits?<param1>=<value1> HTTP/1.1
Content-Type: application/json; charset=utf-8
Authorization: Bearer <JWT_TOKEN_HERE>
```

### Query Parameters

Parameter | Required | Type | Description
--------- | ------- | ----------- | -------
status | true | string | The kits status to filter results. Allowed values: ['registered', 'processed', 'canceled']


> Response Definition

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

```json
[
    {
        "kit_id": "ABCDEF4567",
        "order_number": "RB6E2BEA57E27456BA53D3A2D63125A5",
        "status": "registered"
    },
    {
        "kit_id": "ABCDEF8910",
        "order_number": "RC1223G123EA57E271231412312412YY",
        "status": "registered"
    }
]
```