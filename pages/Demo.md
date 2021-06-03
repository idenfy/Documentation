# i'Denfy demo API

In order for you to start using our demo API you will need two things – ***API key*** and ***API secret***. Both can be retrieved by contacting *iDenfy support* or *iDenfy sales team*. Emails are given below:
- sales@idenfy.com
- support@idenfy.com
- info@idenfy.com

### In demo available:

- Register client
- Generate token 
- Set receive token
- Send identification status 

#### Register client:

Register new client to idenfy.com and send email about successful registration. Also generate identification token and add 8 digit code to registration email.

Send a *HTTP Post* request to: [https://demo.idenfy.com/api/send-registration](https://demo.idenfy.com/api/send-registration)

The request must contain *basic auth* headers where *username* is *api key* and *password* is *api secret*.<br>

The request must contain JSON with email and parameters for generating identification token, described in [Parameters for identification token](https://github.com/idenfy/Documentation/blob/master/pages/GeneratingIdentificationToken.md#sending-request).

|Key       |Required|Type          |Explanation|
|----------|--------|--------------|-----------|
|`email`   |Yes     |`String`      | Client email address.|


##### Example request

```json
{  
   "email": "client_email@email.com",
   "clientId":"100000",
   "firstName":"John Tom",
   "lastName":"Smith"
}
```

##### Example response

```json
{
    "message": "Token created and registration email sent."
}
```

#### Generate token:

Create identification token.

Send a *HTTP Post* request to: [https://demo.idenfy.com/api/generate-token](https://demo.idenfy.com/api/generate-token)

The request must contain *basic auth* headers where *username* is *api key* and *password* is *api secret*.<br>

The request must contain JSON with email and parameters for generating identification token, described in [Parameters for identification token](https://github.com/idenfy/Documentation/blob/master/pages/GeneratingIdentificationToken.md#sending-request).

|Key       |Required|Type          |Constraints|Explanation|
|----------|--------|--------------|-----------|-----------|
|`email`   |Yes     |`String`      | -         | Client email address.|

##### Example request

```json
{  
   "email": "client_email@email.com",
   "clientId": "100000",
   "firstName": "John Tom",
   "lastName": "Smith"
}
```

##### Example response

```json
{
    "message": "Token created successfully",
    "authToken": "oO1M2X5vQG64L40Dp13P6LsgJ2JDnUwCuszmIZJT",
    "scanRef": "1fa846ae-021d-11eb-82ab-03252165b3af",
    "digitString": "85505667",
    "clientId": "123",
    "personScanRef": "123",
    "firstName": "John Tom",
    "lastName": "Smith",
    "successUrl": null,
    "errorUrl": null,
    "unverifiedUrl": null,
    "locale": null,
    "country": null,
    "expiryTime": 3600,
    "sessionLength": 3600,
    "documents": [
        "ID_CARD",
        "PASSPORT",
        "RESIDENCE_PERMIT"
    ],
    "dateOfBirth": null,
    "dateOfExpiry": null,
    "dateOfIssue": null,
    "nationality": null,
    "personalNumber": null,
    "documentNumber": null,
    "sex": null,
    "address": null,
    "tokenType": "IDENTIFICATION",
    "videoCallQuestions": []
}
```

#### Set receive token:

Set a receive token for sending notifications to a mobile device by scan-ref or auth token.

Send a *HTTP Post* request to: [https://demo.idenfy.com/api/set-receiver-token](https://demo.idenfy.com/api/set-receiver-token)

The request must contain *receiverToken* and *authToken* or *scanRef*:

|Key             |Required|Type          |Constraints|Explanation|
|----------------|--------|--------------|-----------|-----------|
|`receiverToken` |Yes     |`String`       |-          |A mobile recipient token for notifications.|
|`authToken`     |Yes     |`String`       |-          |A unique string for identification process (will be passed as a url parameter when redirecting a client to identification platform).|
|`scanRef`       |Yes     |`String`       |-          |A unique string identifying a client identification.|


##### Example request

```json
{  
   "receiverToken": "12345678",
   "authToken": "pgYQX0z2T8mtcpNj9I20uWVCLKNuG0vgr12f0wAC"
}
```

```json
{  
   "receiverToken": "12345678",
   "scanRef": "ec6a7108-8c26-11e9-9758-309c231b1bac"
}
```

##### Example response

```json
{
    "message": "Receiver token set."
}
```

#### Send identification status:

Send identification status after manual review to demo client by email and mobile notification.

Send a *HTTP Post* request to: [https://demo.idenfy.com/api/send-identification](https://demo.idenfy.com/api/send-identification)

The request must contain JSON with parameters:

|Key         |Required|Type          |Constraints      |Explanation|
|------------|--------|--------------|-----------------|-----------|
|`scanRef`   |Yes     |`String`      |                 |A unique string identifying a client identification.|
|`faceStatus`|Yes     |`String`      |- Max length 30  |A face analysis result (decision made by a automatic system and human). Possible values:<br>- FACE_MATCH<br>- FACE_MISMATCH<br>- NO_FACE_FOUND<br>- TOO_MANY_FACES<br>- FACE_TOO_BLURRY<br>- FACE_UNCERTAIN<br>- FACE_NOT_ANALYSED<br>- FACE_ERROR<br>- AUTO_UNVERIFIABLE<br>- FAKE_FACE<br>[For value explanations refer to status vocabulary](https://github.com/idenfy/Documentation/blob/master/pages/Vocabulary.md#identification-status-values-vocabulary).  |
|`docStatus` |Yes     |`String`      |- Max length 30  |A document analysis result (decision made by a automatic system and human). Possible values:<br>- DOC_VALIDATED<br>- DOC_INFO_MISMATCH<br>- DOC_NOT_FOUND<br>- DOC_NOT_FULLY_VISIBLE<br>- DOC_NOT_SUPPORTED<br>- DOC_FACE_NOT_FOUND<br>- DOC_TOO_BLURRY<br>- DOC_FACE_GLARED<br>- MRZ_NOT_FOUND<br>- MRZ_OCR_READING_ERROR<br>- DOC_EXPIRED<br>- COUNTRY_MISMATCH<br>- DOC_TYPE_MISMATCH<br>- DOC_DAMAGED<br>- DOC_FAKE<br>- DOC_ERROR<br>- AUTO_UNVERIFIABLE<br>- DOC_NOT_ANALYSED<br>- DOC_NAME_ERROR<br>- DOC_SURNAME_ERROR<br>- DOC_EXPIRY_ERROR<br>- DOC_DOB_ERROR<br>- DOC_PERSONAL_NUMBER_ERROR<br>- DOC_NUMBER_ERROR<br>- DOC_DATE_OF_ISSUE_ERROR<br>- DOC_SEX_ERROR<br>- DOC_NATIONALITY_ERROR<br>[For value explanations refer to status vocabulary](https://github.com/idenfy/Documentation/blob/master/pages/Vocabulary.md#identification-status-values-vocabulary).|

##### Example request

```json
{  
   "scanRef": "ec6a7108-8c26-11e9-9758-309c231b1bac",
   "faceStatus": "FACE_MATCH",
   "docStatus": "DOC_VALIDATED"
}
```

##### Example response

```json
{
    "message": "Identification sent."
}
```
