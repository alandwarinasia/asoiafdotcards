## Transformers.cards API ##

Transformers.cards card data is stored in an Airtable database, which can be queried using a built-in API. Using this API, you can integrate Transformers.cards data with any external system or application. The API closely follows REST semantics, uses JSON to encode objects, and relies on started HTTP codes to signal operation outcomes.

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

You can authenticate to the API key in the HTTP authorization bearer token header. Alternatively, a slightly lower-security approach is to provide your API key with the `api_key` query parameter.
