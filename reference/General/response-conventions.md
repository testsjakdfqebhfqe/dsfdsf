---
title: Response Conventions
excerpt: Success or error, it's easy to tell.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
> 📘 Format
>
> Responses are always going to be json, unless specified otherwise.

## Successful Response

You should see the following response structure when you provide a valid request, that does not error out. 

```json
{
  "body": {
    "examples": [
      {
        "PK": "123abc",
        "ts": 1665556443,
        "name": "Cheese",
      }
    ]
  },
  "success": true,
  "message": "Optional message goes here"
}
```

* Successful responses will have a `success:true` bool set.
* When data is returned, it's in the `body.controllerName` array. Above assumes "examples" controller. 
* Every unique object has a primary key, denoted by the `PK` field. 

## Failure / Error

If you receive an error, it will look like this.

```json
{
    "body": [],
    "success": false,
    "error": {
        "message": "Error message goes here",
        "code": _ERROR_CODE_
    }
}
```

* Error responses will have a `success:false` bool set. 
* `body` will be an empty array.
* `error` object will contain `message` and `code`.
* First 3 digits of the error code will match the HTTP status code.
