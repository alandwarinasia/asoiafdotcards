## Transformers.cards API ##

Transformers.cards card data is stored in an Airtable database, which can be queried using a built-in API. Using this API, you can integrate Transformers.cards data with any external system or application. The API closely follows REST semantics, uses JSON to encode objects, and relies on started HTTP codes to signal operation outcomes.

### Warning Experimental ###

The Transformers.cards API is currently in an experimental 'alpha' phase and is not yet generally available. If you are a developer interested in leveraging the card data for a third-party application (and are comfortable dealing with some jank), send me a message!

### Clients ###

Your application will need an Airtable API client.

- JavaScript: [airtable.js](https://github.com/Airtable/airtable.js) (Official)
- Ruby: airtable
- Ruby: airrecord
- .NET: airtable.net
