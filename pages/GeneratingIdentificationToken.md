# Generating a token

If you have ***API key*** and ***API secret*** you can create an identification token.
### Sending request
Send a *HTTP Post* request to: [https://ivs.idenfy.com/api/v2/token](https://ivs.idenfy.com/api/v2/token)<br>
The request must contain *basic auth* headers where *username* is *api key* and *password* is *api secret*.<br>
The request must contain JSON with optional and mandatory parameters:

|Key|Required|Explanation|Type|Constraints<img width=/>|Default value|
|---|---|---|---|---|---|
|`clientId`|Yes|A unique string identifying a client.|String|- Not null<br>- Max length 100<img width=750/>|-|
|`firstName`|No|A name(s) of a client to be identified.|String|- Min length 1<br>- Max length 100 <br>- Not digits <br>- Not characters: ~!@#$%^*()_+={}[]\|:;",<>/? |-|
|`lastName`|No|A surname(s) of a client to be identified.|String|- Min length 1<br>- Max length 100 <br>- Not digits <br>- Not characters: ~!@#$%^*()_+={}[]\|:;",<>/?|-|
|`successUrl`|No|A url where a client will be redirected after a successful identification.|String|- Min length 5<br>- Max length 2048|`https://`<br>`ui.idenfy.com/`<br>`result?status=success`|
|`errorUrl`|No|A url where a client will be redirected after a failed identification.|String|- Min length 5<br>- Max length 2048|`https://`<br>`ui.idenfy.com/`<br>`result?status=fail`|
|`unverifiedUrl`|No|A url where a client will be redirected after a not analyzed identification. E.g. user immediately cancels process.|String|- Min length 5<br>- Max length 2048|`https://`<br>`ui.idenfy.com/`<br>`result?status=unverified`|
|`locale`|No|A country code in alpha-2 format. Determines what default language a client will see in identification UI.|String|- Values:<br>&nbsp;&nbsp;&nbsp;&nbsp;-`lt`<br>&nbsp;&nbsp;&nbsp;&nbsp;-`en`<br>&nbsp;&nbsp;&nbsp;&nbsp;-`ru`<br>&nbsp;&nbsp;&nbsp;&nbsp;-`pl`<br>&nbsp;&nbsp;&nbsp;&nbsp;-`ro`<br>&nbsp;&nbsp;&nbsp;&nbsp;-`lv`|`en`|
|`expiryTime`|No|Length of time in seconds after which a newly generated token will become invalid.|Integer|- More than 0|`3600`|
|`sessionLength`|No|Length of time in seconds where a client is given to identify himself in indentification UI.|Integer|- More than 60<br>- Less than 3600|`600`|
|`country`|No|A default document country in alpha-2 code for a client. A client will not be able to select a different country.|String|- Any country in alpha-2 code|`null`|
|`documents`|No|Supported identification documents for the client.|List\[String\]|- Values:<br>&nbsp;&nbsp;&nbsp;&nbsp;-`ID_CARD`<br>&nbsp;&nbsp;&nbsp;&nbsp;-`PASSPORT`<br>&nbsp;&nbsp;&nbsp;&nbsp;-`RESIDENCE_PERMIT`<br>&nbsp;&nbsp;&nbsp;&nbsp;-`DRIVER_LICENSE`<br>&nbsp;&nbsp;&nbsp;&nbsp;-`OTHER`|- Values:<br>&nbsp;&nbsp;&nbsp;&nbsp;-`ID_CARD`<br>&nbsp;&nbsp;&nbsp;&nbsp;-`PASSPORT`|
|`dateOfBirth`|No|Date of birth of a client.|String|- Format: YYYY-MM-DD|`null`|
|`dateOfExpiry`|No|Date of expiry of a client document.|String|- Format: YYYY-MM-DD|`null`|
|`dateOfIssue`|No|Date of issue of a client document.|String|- Format: YYYY-MM-DD|`null`|
|`nationality`|No|Nationality of a client.|String|- Any country in alpha-2 code|`null`|
|`personalNumber`|No|Personal/national number of a client.|String|- Min length 1|`null`|
|`documentNumber`|No|Number of a client document.|String|- Min length 1|`null`|
|`sex`|No|Gender of a client.|String|- Values:<br>&nbsp;&nbsp;&nbsp;&nbsp;-`M`<br>&nbsp;&nbsp;&nbsp;&nbsp;-`F`|`null`|
### Receiving response
The response JSON contains exact same fields as JSON during token generation. It also returns default values for fields
that were optional and not specified during token generation. Additionally, the response also provides these fields below.

|Key|Explanation|Constraints|Example value|
|---|---|---|---|
|`message`|A message for a developer about the status of generated token.|- Max length 100<img width=375/>|`"Token created successfully"`
|`authToken`|A unique string for identification process (will be passed as a url parameter when redirecting a client to identification platform).|- Length <= 40|`"3FA5TFPA2ZE3LMPGGS1EGOJNJE"`
|`scanRef`|A unique string identifying a client identification on iDenfy’s side.|- Length <= 40|`"d2714c8a-ec05-11e8-834f-067891e3383a"`
|`clientId`|A unique string identifying a client on your companies side. (The same value when requesting to generate a token)|- Not null<br>- Max length 100|`"5F7E4FR14"`

### Graphical representation of token generation (UML activity)

<img src="https://raw.githubusercontent.com/idenfy/Documentation/master/resources/TokenGenerationUmlActivityDiagram.jpg" alt="Token generation UML activity diagram" width="450">

### Examples
#### Example requests

You can choose not to send any data regarding your client that needs to be identified. The only mandatory parameter is **clientId**.
```json
{  
   "clientId":"100000"
}
```
As our only mandatory parameter is **clientId**, however we strongly recommend that you would append at least client’s name and surname if possible. It increases the success rate of identification verification.
```json
{  
   "clientId":"100000",
   "firstName":"John Tom",
   "lastName":"Smith"
}
```
Specify all of the parameters for full control.
```json
{  
   "clientId":"100000",
   "firstName":"John Tom",
   "lastName":"Smith",
   "successUrl":"https://www.my-company.com/idenfy/success",
   "errorUrl":"https://www.my-company.com/idenfy/fail",
   "locale":"en",
   "expiryTime":600,
   "sessionLength":600,
   "country":"lt",
   "documents":["PASSPORT", "OTHER"],
   "dateOfBirth": "1990-12-20",
   "dateOfExpiry": "1990-12-20",
   "dateOfIssue": "1990-12-20",
   "nationality": "lt",
   "personalNumber": "123456789",
   "documentNumber": "123456",
   "sex": "M"
}
```

#### Example responses
If supplied data in JSON and ***API key*** with ***API secret*** are valid, you should receive a successful response providing you ***scanRef*** which is the main identifier of an identification in *iDefny* platform.

##### An example response with all fields provided:
```json
{
   "message": "Token created successfully",
   "authToken": "pgYQX0z2T8mtcpNj9I20uWVCLKNuG0vgr12f0wAC",
   "scanRef": "ec6a7108-8c26-11e9-9758-309c231b1bac",
   "clientId": "100000",
   "firstName": "JOHN TOM",
   "lastName": "SMITH",
   "successUrl": "https://www.my-company.com/idenfy/success",
   "errorUrl": "https://www.my-company.com/idenfy/fail",
   "locale": "en",
   "country": "lt",
   "expiryTime": 600,
   "sessionLength": 600,
   "documents": [
     "PASSPORT",
     "OTHER"
   ],
   "dateOfBirth": "1990-12-20",
   "dateOfExpiry": "1990-12-20",
   "dateOfIssue": "1990-12-20",
   "nationality": "lt",
   "personalNumber": "123456789",
   "documentNumber": "123456",
   "sex": "M"
}
```

##### An example response with no fields provided:
```json
{
  "message": "Token created successfully",
  "authToken": "LEWCd6xHTW2auHrst9MEqZN8tUgKsUQ8hSMNYoLI",
  "scanRef": "9b11acb2-8c27-11e9-9758-309c231b1bac",
  "clientId": "100000",
  "personScanRef": "100000",
  "firstName": null,
  "lastName": null,
  "successUrl": null,
  "errorUrl": null,
  "locale": "en",
  "country": null,
  "expiryTime": 3600,
  "sessionLength": 300,
  "documents": [
    "ID_CARD",
    "PASSPORT",
    "RESIDENCE_PERMIT",
    "DRIVER_LICENSE",
    "OTHER"
  ],
  "dateOfBirth": null,
  "dateOfExpiry": null,
  "dateOfIssue": null,
  "nationality": null,
  "personalNumber": null,
  "documentNumber": null,
  "sex": null
}
```
Note that in case of a malformed JSON body or API key/secret mismatch you will receive a standard *iDenfy* API error response. For more on *iDenfy* API responses visit [iDenfy error messages](https://github.com/idenfy/Documentation/blob/master/pages/StandardErrorMessages.md).
