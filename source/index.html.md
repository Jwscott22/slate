---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - http

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Graze API guide. You can use these API endpoints to integrate with external services and expose selected Moogsoft AIOps functionality to authorized external clients.

You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Configuration

The Graze API is implemented as a set of servlets running in the Moogsoft AIOps Tomcat instance that handles external Graze requests, making the UI servlet calls directly via cross-contexts. 

Tomcat must be configured to allow cross-context calls to be made by adding the following to the context.xml file in the Tomcat $APPSERVER_HOME/conf directory:
```http
<Context crossContext="true">
```

# Authentication

The Graze API supports basic authentication. You can use the default Grazer user credentials for this:

```http
username: graze
password: graze
```

All Graze requests use the following URL format, where server is the hostname of the machine running the UI

```http
https://<server>/graze/v1/authenticate
```

Make sure to replace `<server>` with your instance name.

# Alerts

## addAlertCustomInfo

A POST request to add and merge custom information for a specified alert.
```shell
curl -X POST -u graze:graze -k -v "https://localhost/graze/v1/addAlertCustomInfo" -H "Content-Type: application/json; charset=UTF-8" -d '{"alert_id" : 9, "custom_info" : { "field1" : "value2" , "field2" : "value2" , "field3" : ["item1","item2","item3"] , "field4" : {"field4-1" : "value4-1","field4-2" : "value4-2"} }}'
```
> This endpoint returns an HTTP status code.

### HTTP Request

`POST http://example.com/graze/v1/addAlertCustomInfo`

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
auth_code | String | Valid auth_token returned from the authenticate request.
alert_id | Number | Valid alert ID
custom_info | JSON | A JSON Object containing the custom information.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

# HTTP Status Codes
The Graze API returns the following HTTP status and error codes:

HTTP Code | Description 
-------------- | -------------- 
200 | Success
400 | Bad Request
401 | Unauthorised/Invalid auth_code
403 | Forbidden Request
500 | Failed Request*

*A failed request might occur if the sitn_id is invalid for example.

