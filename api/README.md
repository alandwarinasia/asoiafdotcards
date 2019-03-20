## Transformers.cards API ##

### Overview ###
Transformers.cards card data is stored in an Airtable database, which can be queried using a built-in API. Using this API, you can integrate Transformers.cards data with any external system or application. The API closely follows REST semantics, uses JSON to encode objects, and relies on started HTTP codes to standard operation outcomes.

### Warning: Experimental! ###
The Transformers.cards API is currently in an experimental 'alpha' phase and is not yet generally available. If you are a developer interested in leveraging the card data for a third-party application (and are comfortable dealing with some jank), send me a message!

### Clients ###
There are a number of Airtable API clients available, none of which are developed by me:

* JavaScript: [airtable.js](https://github.com/Airtable/airtable.js) (Official)
* Ruby: [airtable](https://github.com/Airtable/airtable-ruby)
* Ruby: [airrecord](https://github.com/sirupsen/airrecord)
* .NET: [airtable.net](https://github.com/ngocnicholas/airtable.net)

### Rate Limits ###
The API is currently limited to 5 requests per second, per API key. If you exceed this rate, you will recieve a 429 status code and will need to wait 30 seconds before subsequent requests will succeed. The official Node.js client has built-in retry logic.

If you anticipate a higher read volume, we recommend using a caching proxy.

### Authentication ###
The API uses simple token-based authentication. Currently, there is no way for you to independently generate an API key. Contact me on Twitter or Discord and I will generate one for you.

You can authenticate to the API key in the HTTP authorization bearer token header:

```
$ curl https://api.airtable.com/v0/appVjmNG3AukyOaQn/Bot%20Cards \
-H "Authorization: Bearer YOUR_API_KEY"
```
 Alternatively, a slightly lower-security approach is to provide your API key with the `api_key` query parameter:

```
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

## Errors ##
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

### Support ###
I'm not currently equipped to guarantee or offer full-time support for this, but if you run into an issue, jump into the Transformers.cards [Discord](https://discordapp.com/invite/dMzBjfD) server and probably I or another dev can help you out.

#### Available Data ####
Currently the data contained in the `Bot Cards` and the `Battle Cards` tables of the Transformers.cards database are available in the API. The sections below describe the fields contained within a 'record' (which is an object in the database that represents a specific card). If you have used the filters or sorting parameters on Transformers.cards before, these should already be familiar to you.

### Bot Cards ###

A `Bot Card` is typically represented by the following JSON object:

```
{
    "id": "recTiwJ952L2P2f9D",
    "fields": {
        "Name": "Arcee",
        "Image": [
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
            },
            {
                "id": "att2nN8nYDZYzYzJD",
                "url": "https://dl.airtable.com/.attachments/45c0369427a9ef624bec8812d76fa7f7/a380e39a/arcee-skilled-fighter-alt.png",
                "filename": "arcee-skilled-fighter-alt.png",
                "size": 334875,
                "type": "image/png",
                "thumbnails": {
                    "small": {
                        "url": "https://dl.airtable.com/.attachmentThumbnails/5d9862a54d0456a5c28fc0f3221b2e11/3515c420",
                        "width": 26,
                        "height": 36
                    },
                    "large": {
                        "url": "https://dl.airtable.com/.attachmentThumbnails/c244c947c742d0b33002199769d1fe6c/99da01dc",
                        "width": 512,
                        "height": 723
                    },
                    "full": {
                        "url": "https://dl.airtable.com/.attachmentThumbnails/492c10b4c4314d396a5eaf8a6572a9db/bdccfe91",
                        "width": 710,
                        "height": 1002
                    }
                }
            }
        ],
        "Subtitle": "Skilled Fighter",
        "⭐": 5,
        "Affiliation": "Autobot",
        "Set": "Wave 1",
        "Card Number": "T01/T40",
        "Rarity": "Rare",
        "Card Text": "Alt Mode:\nWhen you flip to this mode > Repair 1 damage from each of your characters.\n\nBot Mode:\nThis has pierce equal to her ATK.",
        "🧡": 9,
        "Alt⚔️": 2,
        "Bot⚔️": 1,
        "Alt🛡️": 1,
        "Bot🛡️": 1,
        "Alt Type": [
            "Motorcycle"
        ],
        "Roles": [
            "Specialist"
        ]
    },
    "createdTime": "2019-02-06T00:41:14.000Z"
}
```

#### Fields ####

Each record in the `Bot Cards` table contains the following fields, in addition to its unique `id`:

| Field Name | Field Type | Description | 
| ------ | ------ | ------ |
| `Name` | `string` | A single line of text, representing the name of the card, sans subtitle. |
| `Image` | `array of attachment objects` | Each attachment object (image associated with a card) may contain the following properties:  `id` (unique image id);  `url` (an https url to the image ending in foo.png); `filename` (foo.png); `size` (file size of foo.png, in bytes); `type` (content type, e.g. "image/png"); `width` (of foo.png, in pixels); `height` (of foo.png, in pixels), `thumbnails` (`url`, `width`, and `height` data for three sizes of thumbnails of the previously enumerated `filename`). |
| `Subtitle` | `string` | A single line of text, representing the card's subtitle. |
| WIP | 

### Battle Cards ###

A `Battle Card` is represented by the following JSON object:

```
{
    "id": "recRBzdbpSNDxdpix",
    "fields": {
        "Name": "Aerial Recon",
        "Image": [
            {
                "id": "attAE07rDIVfJBU4K",
                "url": "https://dl.airtable.com/.attachments/9e24c05dc3bf637a33d1442ced521cae/f4060870/aerialrecon.png",
                "filename": "Front",
                "size": 320706,
                "type": "image/png",
                "thumbnails": {
                    "small": {
                        "url": "https://dl.airtable.com/.attachmentThumbnails/5c5de279f073e583d6a7773df13807a4/8cfcc6c9",
                        "width": 26,
                        "height": 36
                    },
                    "large": {
                        "url": "https://dl.airtable.com/.attachmentThumbnails/620826a5f3aa6034a72945f56b94bbf5/2f076004",
                        "width": 371,
                        "height": 519
                    },
                    "full": {
                        "url": "https://dl.airtable.com/.attachmentThumbnails/539d95398c50cb8b934472a382154711/4b17c4a4",
                        "width": 371,
                        "height": 519
                    }
                }
            }
        ],
        "Set": "Wave 1",
        "Battle Icons": [
            "1"
        ],
        "Card Type": "Upgrade",
        "Sub-Type": "Utility",
        "Card Text": "Put on Planes only.\n\nWhen the upgraded character attacks or defends → Look at the top card of your deck. You may scrap it.",
        "Rarity": "Uncommon",
        "⭐": 0,
        "⚔️Δ": 0,
        "🛡️Δ": 1,
        "Card Number": "001/081"
    },
    "createdTime": "2019-02-06T11:07:05.000Z"
}
```



#####

Each record in the `Battle Cards` table contains the following fields, in addition to its unique `id`:

| Field Name | Field Type | Description | 
| ------ | ------ | ------ |
| WIP | 

#### Listing Records #####

To list records in `Bot Cards`, issue a **GET** request to the ```Bot Cards``` endpoint:

```
curl "https://api.airtable.com/v0/appVjmNG3AukyOaQn/Bot%20Cards" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

To list records in `Battle Cards`, issue a **GET** request to the ``Battle Cards``` endpoint:

```
curl "https://api.airtable.com/v0/appVjmNG3AukyOaQn/Battle%20Cards" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

Returned records do not include any fields with "empty" value, e.g. `""`,`[]`, or `false`.

You can use the following URL encoded parameters to filter, sort, and format the results:

| Parameter | Data Type | Description |
| ------ | ------ | ------ |
| `fields` | `array of strings` | Only data for fields whose names are in this list will be included in the records. If you don't need every field, you can use this parameter to reduce the amount of data transferred. |
| `maxRecords` | `number` | The maximum total number of records that will be returned in your requests. If this value is larger than `pageSize` (which is 100 by default), you may have to load multiple pages to reach this total. See the Pagination section below for more. |
| `pageSize` | `number` | The number of records returned in each request. Must be less than or equal to 100. Default is 100. See the Pagination section below for more. |
| `sort` | `array of objects`  | A list of sort objects that specifies how the records will be ordered. Each sort object must have a `field` key specifying the name of the field to sort on, and an optional direction key that is either `asc` or `desc`. The default direction is `asc`. For example, to sort records by Name in descending order, send these two query parameters: `?sort%5B0%5D%5Bfield%5D=Name&sort%5B0%5D%5Bdirection%5D=desc` |

#### Retrieve A Specific Card Record ####
To retrieve an existing record in `Bot Cards` table, issue a **GET** request to the record's endpoint. e.g. to retrieve Arcee:

```
curl https://api.airtable.com/v0/appVjmNG3AukyOaQn/Bot%20Cards/recTiwJ952L2P2f9D \
  -H "Authorization: Bearer YOUR_API_KEY"
 ```
Any "empty" fields (e.g. "", [], or false) in the record will not be returned. In attachment objects included in the retrieved record (`Image`), only `id`, `url`, and `filename` are always returned. Other attachment properties may not be included.


#### Pagination ####

The server returns one page of records at a time. Each page will contain `pageSize` records, which is 100 by default.

If there are more records, the response will contain an `offset`. To fetch the next page of records, include `offset` in the next request's parameters.

Pagination will stop when you've reached the end of your table. If the `maxRecords` parameter is passed, pagination will stop once you've reached this maximum.
