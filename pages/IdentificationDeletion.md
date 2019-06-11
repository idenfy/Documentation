# Deleting client data

If you have ***API key*** and ***API secret*** you can delete client data belonging to you. Calling this endpoint will
remove data from iDenfy's system such as: client photos of their document and face, information such as parsed document
information, names, surnames, etc.

### Sending request
Send a *HTTP Post* request to: [https://ivs.idenfy.com/api/v2/delete](https://ivs.idenfy.com/api/v2/delete)<br>
The request must contain *basic auth* headers where *username* is *api key* and *password* is *api secret*.<br>
The request must contain JSON with a scanRef:

|Key|Required|Explanation|Type|Constraints<img width=/>|
|---|---|---|---|---|
|`scanRef`|Yes|A unique string identifying a client on iDenfy’s side.|`String`|- Not null|


### Examples
#### Example request

```json
{
	"scanRef": "350e2420-8850-11e9-baa5-309c231b1bac"	
}
```

#### Example responses
For successful API calls, which correctly delete all data, there will be no message, just a response with a positive **200** status.


##### An example response that failed
Failed API calls will return a message containing, identifying the problem.

```json
{
  "message": "Token has not expired yet.",
  "identifier": "PARTNER_ERROR",
  "documentation": "https://github.com/idenfy/Documentation",
  "severity": "NOT_SEVERE"
}
```
Note that in case of a malformed JSON body or API key/secret mismatch you will receive a standard *iDenfy* API error response. For more on *iDenfy* API responses visit [iDenfy error messages](https://github.com/idenfy/Documentation/blob/master/pages/StandardErrorMessages.md).
