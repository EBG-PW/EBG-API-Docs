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

## POST new contace request

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

# Serverstatus

## GET all stats

```javascript
const Joi = require('joi');

const GetSchema = Joi.object({
    name: Joi.string().trim(),
    type: Joi.string().trim(),
    Country: Joi.string().trim(),
    limit: Joi.number()
});
```

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
name | false | String | Filter servers by name.
type | false | String | Filter servers by type.
Country | false | String | Filter servers by country.
limit | false | Number | Limit the results.


```javascript
const axios = require('axios');

axios.get('/serverstatus?limit=1')
  .then(function (response) {
    // handle success
    console.log(response);
  })
  .catch(function (error) {
    // handle error
    console.log(error);
  })
```

> The above command returns JSON structured like this:

```json
{
  "timespamp":"1602445037",
  "servers":[
    {
    "name":"SRV-OWL-01",
    "type":"Dedicated",
    "host":"ANSF",
    "location":"AT - Linz",
    "online4":true,
    "online6":false,
    "uptime":"30 days",
    "load":0,
    "network_rx":14747, //In bit/s
    "network_tx":265446, //In bit/s
    "cpu":0, //IN % of total CPU (0-100)
    "memory_total":100496656, //In KB
    "memory_used":38702832, //In KB
    "swap_total":115176720, //In KB
    "swap_used":39049380, //In KB
    "hdd_total":3528493, //In MB
    "hdd_used":847982, //In MB
    "custom":""
    }
  ]
}
```

### HTTP Request

`GET https://api.ebg.pw/api/v1/serverstatus`

<aside class="success">
Returns <code>200</code> and a json.
</aside>

<aside class="warning">
Returns <code>503</code>. When that happens the API can´t find stats.json
</aside>

<aside class="notice">
API Limit is 60 requests per 1 minute per IP. Invalid requests also count to this value!
</aside>

## GET overview stats

```javascript
const Joi = require('joi');

const GetSchemaNow = Joi.object({
    all: Joi.boolean()
});
```

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
all | false | bool | If true, it will return all devices including personal pcs
bundle | false | bool | If true, all WCG servers will be displayed as one

```javascript
const axios = require('axios');

axios.get('/serverstatus/now')
  .then(function (response) {
    // handle success
    console.log(response);
  })
  .catch(function (error) {
    // handle error
    console.log(error);
  })
```

> The above command returns JSON structured like this:

```json
{
  "timespamp":"1602445037",
  "online":"10", //10 Servers are online
  "offline":"2", //2 Servers are offline
  "hardware":
    {
    "CPUtotal":1000, //10 servers are running right now, 1000% is max
    "CPUused":"117.00", //Usage of all 10 Servers with the limit above
    "RAMtotal":426243164, //In KB
    "RAMused":164287376, //In KB
    "DISKtotal":22038787, //In MB
    "DISKused":12604126, //In MB
    "NETrx":122390, //In bit/s
    "NETtx":66168} //In bit/s
    },
  "onlineservers":"[]", //List of all servers that are online
  "offlineservers":"[]" //List of all servers that are offline
}
```

### HTTP Request

`GET https://api.ebg.pw/api/v1/serverstatus/now`

<aside class="success">
Returns <code>200</code> and a json.
</aside>

<aside class="warning">
Returns <code>503</code>. When that happens the API can´t find stats.json
</aside>

<aside class="notice">
API Limit is 60 requests per 1 minut per IP. Invalid requests also count to this value!
</aside>

# MSH-ConfigGenerator

## MSH v2.3.3

```javascript
const Joi = require('joi');

const GetSchema = Joi.object({
	FileName: Joi.string().max(128).required().regex(/^[a-z\d\s\-\.\,\ä\ü\ö\ß\&]*$/i),
	ServerType: Joi.string().max(32).required().regex(/^[a-z\d\s\-\.\,\ä\ü\ö\ß\&]*$/i),
	Version: Joi.string().max(16).required().regex(/^[0-9\-\.]*$/),
	RAM: Joi.number().max(524288).required(),
	Port: Joi.number().max(65535).required(),
	StopTime: Joi.number().max(86400).required()
})
```

This config generator only works for FULL RELEASES of minecraft.  
This is for MSH version 2.3.3

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
FileName | true | String | The name of the minecraft server jar
ServerType | true | String | Paper/Forge/Vanilla/...
Version | true | String | Version of minecraft.
RAM | true | Number | Memory for the minecraft server.
Port | true | Number | Port the MSH-Server should listen.
StopTime | true | Number | Time to wait with 0 players befor shutdown

```javascript
const axios = require('axios');

axios.post('/MSH-ConfigGenerator/2-3-3', {
  FileName: "server.jar",
	ServerType: "Paper",
	Version: "1.16.5",
	RAM: 1024,
	Port: 25565,
  StopTime: 120
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```

> The above command returns a JSON File as download structured like this:

```json
{
  "Server":{
    "Folder":"./",
    "FileName":"server.jar",
    "Protocol":"754",
    "Version":"EBG.PW 1.16.5"
  },"Commands":{
    "StartServer":"java -Xmx2048M -Xms128M -jar serverFileName nogui",
    "StopServer":"stop",
    "StopServerForce":"stop"
  },"Msh":{
    "CheckForUpdates":true,
      "Debug":false,
    "HibernationInfo":"                   &fserver status:\n                   &b&lHIBERNATING",
    "Port":"25565",
    "StartingInfo":"                   &fserver status:\n                    &6&lWARMING UP",
    "TimeBeforeStoppingEmptyServer":120
  }
}

```

### HTTP Request

`GET https://api.ebg.pw/api/v1/MSH-ConfigGenerator/2-3-3`

<aside class="success">
Returns <code>200</code> and a json File to download.
</aside>

<aside class="warning">
Returns <code>400</code>.
</aside>

<aside class="notice">
API Limit is 265 requests per 1 minute per IP. Invalid requests also count to this value!
</aside>
