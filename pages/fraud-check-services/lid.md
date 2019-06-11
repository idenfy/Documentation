# Lost & Invalid documents
This service checks whether given person's identity document is not registered as stolen or lost.

#### Pricing
Please contact _iDenfy_ support for a detailed price-sheet.

#### Callback data
The service check returns identity document's data in JSON format.
Overall response can be seen in the table below:

##### Overall response table

|JSON key          |Type        |Explanation                                                |
|------------------|------------|-----------------------------------------------------------|
|`status`          |`Object`    |The overall status of the service check.                   | 
|`data`            |`List`      |Data returned from services.                               |
|`serviceName`     |`String`    |The name of the service that was used to check a person.   |
|`serviceGroupType`|`String`    |The type of the servi  ce that was used. It is always `LID`. |
|`uid`             |`String`    |A unique identifier for a request. NOTE that it is unique only in one request scope. It is not unique globally. This parameter is only useful when doing multi-person checks.|
|`errorMessage`    |`String`    |In case of an error in the checking process a human readable error message is given.|

##### Status table

|JSON key            |Type        |Explanation                                                             |
|--------------------|------------|------------------------------------------------------------------------|
|`serviceSuspected`  |`Bool`      |Indicates whether a service found a record about the person under check.| 
|`checkSuccessful`   |`Bool`      |Indicated whether an error occurred while doing a check.                |
|`serviceFound`      |`Bool`      |Indicates whether a service was found for a given country.              |
|`serviceUsed`       |`Bool`      |Indicated whether a service was used.                                   |
|`overallStatus`     |`String`    |A mapping string indicating overall status of the check.                |

##### Data table
A service response in `data` field returns a list of objects which are detailed in the table below:

|JSON key            |Type        |Explanation                                                |
|--------------------|------------|-----------------------------------------------------------|
|`documentNumber`    |`String`    |Document number in the service's database.                 | 
|`documentType`      |`String`    |Document type in the service's database.                   |
|`valid`             |`Bool`      |Indicated whether document is valid or not.                |
|`expiryDate`        |`String`    |Date when a document expires.                              |

#### Example response

```json
{
    "status": {
        "serviceSuspected": true,
        "checkSuccessful": true,
        "serviceFound": true,
        "serviceUsed": true,
        "overallStatus": "SUSPECTED"
    },
    "data": [
        {
            "documentNumber": "12347539",
            "documentType": "PASSPORT",
            "valid": false,
            "expiryDate": "2018-03-21"
        }
    ],
    "serviceName": "IrdInvalidPapers",
    "serviceGroupType": "LID",
    "uid": "1S1DTTF1IV5FM4D4BO325CG8F",
    "errorMessage": null
}
```
