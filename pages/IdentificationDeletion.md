# Deleting client data

If you have ***API key*** and ***API secret*** you can delete client data belonging to you. Calling this endpoint will
remove data from iDenfy's system such as: client photos of their document and face, information such as parsed document
information, names, surnames, etc.

### Sending request
Send a *HTTP Post* request to: [https://ivs.idenfy.com/api/v2/delete](https://ivs.idenfy.com/api/v2/delete)<br>
The request must contain *basic auth* headers where *username* is *api key* and *password* is *api secret*.<br>
The request must contain JSON with a list of scan-refs:

|Key|Required|Explanation|Type|Constraints<img width=/>|
|---|---|---|---|---|
|`scanRefs`|Yes|A list of unique strings identifying clients on iDenfy’s side.|`List[String]`|- Not null<br>- Min list length 1<br>- Max list length 100<img width=375/>|


### Examples
#### Example request

```json
{
	"scanRefs": [
		"350e2420-8850-11e9-baa5-309c231b1bac",
		"8741acce-8c30-11e9-9758-309c231b1bac",
		"8b4b4b04-8c30-11e9-9758-309c231b1bac"
	]
}
```

#### Example responses
For successful API calls, which correctly delete all data there will be no message, just a response with a positive **200** status.


##### An example response that failed:
Failed API calls will return a message containing the scan-ref that failed, identifying the problem.

```json
{
  "message": "Token has not expired yet. Scan-ref: b586d982-8c31-11e9-9758-309c231b1bac.",
  "identifier": "PARTNER_ERROR",
  "documentation": "https://github.com/idenfy/Documentation",
  "severity": "NOT_SEVERE"
}
```

Notes:

- Deleting a list of identifications and running into an invalid scanRef halfway, will delete all identifications on the list up to that identification.
- In case of a malformed JSON body or API key/secret mismatch you will receive a standard *iDenfy* API error response. For more on *iDenfy* API responses visit [iDenfy error messages](https://github.com/idenfy/Documentation/blob/master/pages/StandardErrorMessages.md).
