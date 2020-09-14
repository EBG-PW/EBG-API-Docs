---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true
---

# Introduction

This is a plugin based API, that means not all methods here are available at all time! You can check loaded plugins at anytime just by going to [/api/v1/](https://api.ebg.pw/api/v1).

Below you will find all official EBG plugins for our API.

# Contacs

## Contacs Query Parameters

```javascript
const Joi = require('joi');

const schema = Joi.object({
	name: Joi.string().trim().required(),
	email: Joi.string().email().required(),
	category: Joi.number().required(),
	person: Joi.number().required(),
	message: Joi.string().trim().required(),
});
```

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
name | true | String | The users name.
email | true | String | The users email.
category | true | Number | Category or the request.
person | true | Number | Determines who should process this request.
message | true | String | Short text of the request.

## Place a contact request

```javascript
const axios = require('axios');

axios.post('/contacs', {
    name: "BolverBlitz",
	email: "demo@ebg.pw",
	category: "1",
	person: "0",
	message: "Your server is burning"
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```

> The above command returns JSON structured like this:

```json
{
    "name": "BolverBlitz",
    "email": "demo@ebg.pw",
    "category": "1",
    "person": 0,
	"message": "Your server is burning"
}

```

### HTTP Request

`POST https://api.ebg.pw/api/v1/contact`

<aside class="success">
Returns <code>200</code> and a json.
</aside>

<aside class="warning">
Returns <code>400</code>.
</aside>

<aside class="notice">
API Limit is 5 requests per 15 minuts per IP. Invalid requests also count to this value!
</aside>
