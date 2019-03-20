## Transformers.cards API ##

### Overview ###
Transformers.cards card data is stored in an Airtable database, which can be queried using a built-in API. Using this API, you can integrate Transformers.cards data with any external system or application. The API closely follows REST semantics, uses JSON to encode objects, and relies on started HTTP codes to standard operation outcomes.

### Warning: Experimental ###
The Transformers.cards API is currently in an experimental 'alpha' phase and is not yet generally available. If you are a developer interested in leveraging the card data for a third-party application (and are comfortable dealing with some jank), send me a message!

### Clients ###
Your application will need an Airtable API client.

* JavaScript: [airtable.js](https://github.com/Airtable/airtable.js) (Official)
* Ruby: [airtable](https://github.com/Airtable/airtable-ruby)
* Ruby: [airrecord](https://github.com/sirupsen/airrecord)
* .NET: [airtable.net](https://github.com/ngocnicholas/airtable.net)

### Rate Limits ###
The API is currently limited to 5 requests per second, per API key. If you exceed this rate, you will recieve a 429 status code and will need to wait 30 seconds before subsequent requests will succeed. The official Node.js client has built-in retry logic.

If you anticipate a higher read volume, we recommend using a caching proxy.

### Authentication ###
The API uses simple token-based authentication. Currently, there is no way for you to independently generate an API key. Contact me on Twitter or Discord and I will generate one for you.


You can authenticate to the API key in the HTTP authorization bearer token header.

```
EXAMPLE USING BEARER TOKEN:
$ curl https://api.airtable.com/v0/appVjmNG3AukyOaQn/Bot%20Cards \
-H "Authorization: Bearer YOUR_API_KEY"
```
 Alternatively, a slightly lower-security approach is to provide your API key with the `api_key` query parameter.

```
EXAMPLE USING QUERY PARAMETER:
$ curl https://api.airtable.com/v0/appVjmNG3AukyOaQn/Bot%20Cards?api_key=YOUR_API_KEY
```

```
EXAMPLE USING CUSTOM CONFIGURATION:
var Airtable = require('airtable');
Airtable.configure({
    endpointUrl: 'https://api.airtable.com',
    apiKey: 'YOUR_API_KEY'
});
var base = Airtable.base('appVjmNG3AukyOaQn');
```

### Errors ###
The API follows HTTP status code semantics. 2xx codes signify success. 3xx mostly represent user errror. 5xx generally correspond to a server error. The error message will return a JSON-encoded body that contains `error` and `message` fields. Those will provide specific error conditions and a human-readable message to identify what caused the error.

#### Success Code ####
`200` OK : Request completed successfully.

#### User Error Codes ####
`400` Bad Request : The request encoding is invalid; the request can't be parsed as valid JSON.

`401` Unauthorized : Accessing a protected resource without authorization or with invalid credentials.

`402` Payment Required : I forgot to pay the hosting bills. My bad.

`403` Forbidden : Accessing a protected resource with API credentials that don't have access to that resource.

`404` Not Found : Route or resource is not found. This error is returned when the request hits an undefined route, or if the resource doesn't exist (or has been deleted).

`413` Request Entity Too Large : The request exceeded the maximum allowed payload size. If you encounter this, let me know.

`422` Invalid Request : The request data is invalid. This includes most of the base-specific validations. You will recieve a detailed error message and code pointing to the exact issue.

#### Server Error Codes ####
`500` Internal Server Error : Something bad happened, but it probably wasn't your fault.

`502` Bad Gateway : The database servers are restarting or an unexpected outage is in progress. This error is generally transitory, and requests are safe to retry.

`503` Service Unavailable : For some reason, the server could not process your request in time. You should retry the request with backoffs.

#### Support ####
I'm not currently equipped to guarantee or offer full-time support for this, but if you run into an issue, jump into the Transformers.cards [Discord](https://discordapp.com/invite/dMzBjfD) server and probably I or another dev can help you out.

#### Available Data ####
Currently the data contained in the `Bot Cards` and the `Battle Cards` tables of the Transformers.cards database are available in the API. The sections below describe the fields contained within a 'record' (which is an object that represents a specific card). If you have used the filters on Transformers.cards they should already be familiar to you.

### Bot Cards ###

Each record in the `Bot Cards` table contains the following fields:


Field Name: `Name`
Field Type: `string`
Description: A single line of text representing the name of the card, sans subtitle.
```
EXAMPLE VALUES:
"Arcee"
"Autobot Cosmos"
"Megatron"
```

Field Name: `Image`
Field Type: `array of attachment objects`
Description: Each attachment object may contain the following properties;
- `id` (unique image id)
- `url` (an https url to the image ending in foo.png)
- `filename` (foo.png)
- `size` (file size of foo.png, in bytes)
- `type` (content type, e.g. "image/png")
- `width` (of foo.png, in pixels)
- `height` (of foo.png, in pixels)
```
EXAMPLE VALUE:
[
    {
        "id": "attdlHVdCrZHZik8T",
        "url": "https://dl.airtable.com/.attachments/a46e0824a82ed546593d6db976eb50a7/8ec79e49/arcee-skilled-fighter-bot.png",
        "filename": "arcee-skilled-fighter-bot.png",
        "size": 381061,
        "type": "image/png",
        "thumbnails": {
            "small": {
                "url": "https://dl.airtable.com/.attachmentThumbnails/53b4ebd109fefebb1b85f9a97102e993/6df1f805",
                "width": 25,
                "height": 36
            },
            "large": {
                "url": "https://dl.airtable.com/.attachmentThumbnails/a7a0d9695cdc5b2ac2c5e25d47ce8911/fdb41cf6",
                "width": 512,
                "height": 734
            },
            "full": {
                "url": "https://dl.airtable.com/.attachmentThumbnails/035ab2e0cbe3cd49c79bd5bce12c5c01/68d23785",
                "width": 702,
                "height": 1006
            }
        }
    }
```

