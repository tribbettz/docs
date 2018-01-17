---
title: Everlywell Enterprise API Reference

language_tabs:
  - http

search: true
---

# Introduction

Documentation for EverlyWell's Enterprise APIs.

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
    "amount": 199.00
}
```

### Query Parameters

Parameter | Required | Type | Description
--------- | ------- | ----------- | -------
amount | true | Double | Total order price

> Response Definition

```http
HTTP/1.1 201 Created
Content-Type: application/json
```

```json
{
    "id": 1,
    "amount": 199.00
}
```



## Get Order

Get an Order by ID.

> Request Definition

```http
GET https://secure.everlywell.com/aapi/v2/orders/<order_id> HTTP/1.1
Content-Type: application/json; charset=utf-8
Authorization: Bearer <JWT_TOKEN_HERE>
```

### Query Parameters

Parameter | Required | Type | Description
--------- | ------- | ----------- | -------
id | true | int | Unique identifier for the Order


> Response Definition

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

```json
{
    "id": 1,
    "state": "processing"
}
```



# Kits API

## Create Kit Registration

Create an Kit Registration for a User.

> Request Definition

```http
POST https://secure.everlywell.com/aapi/v1/kits/<invoice_id>/registration HTTP/1.1
Content-Type: application/json; charset=utf-8
Authorization: Bearer <JWT_TOKEN_HERE>
```

```json
{
    "user": {
        "email": "test@email.com",
        "first_name": "Test",
        "last_name": "Testerson",
        "dob": 1476551410009,
        "phone_number": 5125557485,
        "gender": "male"
    },
    "addresses": [
        {
           "street1": "123 Test str",
           "street2": "",
           "city": "Austin",
           "state": "TX",
           "zipcode": 78701
        }
    ]
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
gender | true | string | Gender of the User associated with the Kit

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
    "kit_id": "1a2b3c4d5e",
    "user_id": 1
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
    "token": "encryptedPayload"
}
```
