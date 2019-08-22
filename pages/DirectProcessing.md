# Direct processing

This endpoint lets you upload customer photos yourself and start processing instantly. The identification token is deactivated after this request.

### Sending request
Send a *HTTP Post* request to: `https://ivs.idenfy.com/api/v2/process`<br>
The request must contain *basic auth* headers where *username* is *api key* and *password* is *api secret*.<br>
The request must contain JSON with these parameters:

|      Key       | Required |              Explanation              |   Type   |                                     Constraints<img width=/>                                     |
| -------------- | -------- | ------------------------------------- | -------- | ------------------------------------------------------------------------------------------------ |
| `authToken`    | Yes      | Identification token                  | `String` | -                                                                                                |
| `country`      | Yes      | Country code in 3166-1 alpha-2 format | `String` | Any country in alpha-2 code                                                                      |
| `documentType` | Yes      | Document type                         | `String` | Possible values:<br>- ID_CARD<br>- PASSPORT<br>- RESIDENCE_PERMIT<br>- DRIVER_LICENSE<br>- OTHER |
| `images`       | Yes      | Images for identification             | `Object` | -                                                                                                |

#### Contents of images

|     JSON key     |   Type   | Can be null |    Constraints    |               Explanation               |
| ---------------- | -------- | ----------- | ----------------- | --------------------------------------- |
| `FRONT`          | `String` | Yes         | - Max size of 2MB | Base64 encoded image of document front  |
| `BACK`           | `String` | Yes         | - Max size of 2MB | Base64 encoded image of document back   |
| `FACE`           | `String` | Yes         | - Max size of 2MB | Base64 encoded image of persons face    |
| `UTILITY_BILL`   | `String` | Yes         | - Max size of 2MB | Base64 encoded image of an utility bill |
| `PASSPORT_COVER` | `String` | Yes         | - Max size of 2MB | Base64 encoded image of passport cover  |

Images required for a specific document should be provided, usually at least `FRONT` and `FACE`.

### Examples
#### Example request

```json
{
    "authToken": "3FA5TFPA2ZE3LMPGGS1EGOJNJE",
    "country": "LT",
    "documentType": "ID_CARD",
    "images": {
        "FRONT":"/9j/4AAQSkZJRgABAQAAAQABAAD/4...",
        "BACK":"/9j/4AAQSkZJRgABAQAAAQABAAD/4...",
        "FACE":"/9j/4AAQSkZJRgABAQAAAQABAAD/4..."
    }
}
```

#### Example responses
For successful API calls, which start the processing, there will be no message, just a response with a positive **200** status.


##### An example response that failed
Failed API calls will return a message identifying the problem.

```json
{
    "message": "No image provided for step 'BACK'",
    "identifier": "MISSING_VALUE",
    "documentation": "https://github.com/idenfy/Documentation",
    "severity": "NOT_SEVERE"
}
```
Note that in case of a malformed JSON body or API key/secret mismatch you will receive a standard *iDenfy* API error response. For more on *iDenfy* API responses visit [iDenfy error messages](https://github.com/idenfy/Documentation/blob/master/pages/StandardErrorMessages.md).