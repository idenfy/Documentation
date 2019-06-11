# AML, PEP & Sanctions, Negative news
This service checks whether given person is in PEP or sanctions list, checks negative news.

#### Pricing
Please contact _iDenfy_ support for a detailed price-sheet.

#### Callback data
The service check returns data associated with the person under check in JSON format.
Overall response can be seen in the table below:

##### Overall response table

|JSON key          |Type        |Explanation                                                |
|------------------|------------|-----------------------------------------------------------|
|`status`          |`Object`    |The overall status of the service check.                   | 
|`data`            |`List`      |Data returned from services.                               |
|`serviceName`     |`String`    |The name of the service that was used to check a person.   |
|`serviceGroupType`|`String`    |The type of the service that was used. It is always `AML`. |
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

##### Data table for AML name check service
A service response in `data` field returns a list of objects which are detailed in the table below:

|JSON key            |Type        |Explanation                                                |
|--------------------|------------|-----------------------------------------------------------|
|`name`              |`String`    |The name of the person in the service's database.          | 
|`surname`           |`String`    |The surname of the person in the service's database.       |
|`nationality`       |`String`    |The nationality of the person in the service's database.   |
|`dob`               |`String`    |The date of birth of the person in the service's database. |
|`suspicion`         |`String`    |Tells the kind of the suspicion.                           |
|`reason`            |`String`    |Tells the reason of the kind of the suspicion.             |
|`score`             |`Integer`   |Confidence coefficient that the information about the person is true.|
|`lastUpdate`        |`String`    |Date of when the record was last updated.                  |
|`isPerson`          |`Bool`      |Indicates whether the record is about a person.            |
|`isActive`          |`Bool`      |Indicated whether a record is active.                      |

##### Data table for AML negative news service
A service response in `data` field returns a list of objects which are detailed in the table below:

|JSON key            |Type        |Explanation                                                |
|--------------------|------------|-----------------------------------------------------------|
|`title`             |`String`    |The title of the news article.                             | 
|`url`               |`String`    |Url pointing to the news article.                          |
|`text`              |`String`    |An short extract of the news article text.                 |
|`type`              |`String`    |The type of the news article.                              |

#### Example response for AML name check service

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
            "name": "NAME",
            "surname": "SURNAME",
            "reason": "LITHUANIA: GOVERNMENT - PRESIDENT",
            "nationality": "LITHUANIA",
            "dob": "1956",
            "suspicion": "PEPS",
            "score": 100,
            "lastUpdate": "2018-10-24",
            "isPerson": true,
            "isActive": true
        },
        {
            "name": "NAME",
            "surname": "SURNAME2",
            "reason": "LITHUANIA: GOVERNMENT - PRESIDENT",
            "nationality": "LITHUANIA",
            "dob": "1956",
            "suspicion": "PEPS",
            "score": 100,
            "lastUpdate": "2018-10-24",
            "isPerson": true,
            "isActive": true
        }
    ],
    "serviceName": "PilotApiAmlV2",
    "serviceGroupType": "AML",
    "uid": "OHT8GR5ESRF5XROWE5ZGCC49A",
    "errorMessage": null
}
```

#### Example response for AML negative news service

```json
{
  "AML": [
    {
      "status": {
        "serviceSuspected": true,
        "serviceUsed": true,
        "serviceFound": true,
        "checkSuccessful": true,
        "overallStatus": "SUSPECTED"
      },
      "serviceName": "PilotApiAmlV2NegativeNews",
      "serviceGroupType": "AML",
      "uid": "Z3LN8T2AU4467DYUTJ3S7PPG1",
      "errorMessage": null,
      "data": [
        {
          "title": "BARACK OBAMA (@BARACKOBAMA) | TWITTER",
          "url": "HTTPS://TWITTER.COM/BARACKOBAMA",
          "text": "THE LATEST TWEETS FROM BARACK OBAMA (@BARACKOBAMA). DAD, HUSBAND, PRESIDENT, CITIZEN. WASHINGTON, DC",
          "type": "NEGATIVE"
        },
        {
          "title": "WELCOME TO THE OBAMA FOUNDATION",
          "url": "HTTPS://WWW.OBAMA.ORG/",
          "text": "-- THE OBAMA FOUNDATION (@OBAMAFOUNDATION) APRIL 26, 2019 A SCHOLAR'S STORY: DR. BONAVENTURE DZEKEM DR. BONAVENTURE DZEKEM IS AN OBAMA FOUNDATION SCHOLAR CURRENTLY STUDYING AT THE UNIVERSITY OF CHICAGO.",
          "type": "NEGATIVE"
        },
        {
          "title": "BARACK OBAMA | THE WHITE HOUSE",
          "url": "HTTPS://WWW.WHITEHOUSE.GOV/ABOUT-THE-WHITE-HOUSE/PRESIDENTS/BARACK-OBAMA/",
          "text": "BARACK OBAMA SERVED AS THE 44TH PRESIDENT OF THE UNITED STATES. HIS STORY IS THE AMERICAN STORY -- VALUES FROM THE HEARTLAND, A MIDDLE-CLASS UPBRINGING IN A STRONG FAMILY, HARD WORK AND EDUCATION ...",
          "type": "NEGATIVE"
        },
        {
          "title": "BARACK OBAMA | FOX NEWS",
          "url": "HTTPS://WWW.FOXNEWS.COM/CATEGORY/PERSON/BARACK-OBAMA",
          "text": "BARACK OBAMA SERVED AS THE 44TH PRESIDENT OF THE UNITED STATES FROM 2009 TO 2017 AND IS THE FIRST AFRICAN-AMERICAN EVER ELECTED TO THE OFFICE. HE IS A MEMBER OF THE DEMOCRATIC PARTY AND PREVIOUSLY ...",
          "type": "NEGATIVE"
        },
        {
          "title": "BARACK OBAMA - U.S. PRESIDENCY, FAMILY & QUOTES - BIOGRAPHY",
          "url": "HTTPS://WWW.BIOGRAPHY.COM/US-PRESIDENT/BARACK-OBAMA",
          "text": "LEARN MORE ABOUT PRESIDENT BARACK OBAMA'S FAMILY BACKGROUND, EDUCATION AND CAREER, INCLUDING HIS 2012 ELECTION WIN. FIND OUT HOW HE BECAME THE FIRST AFRICAN-AMERICAN U.S. PRESIDENT, VIEW VIDEO ...",
          "type": "NEGATIVE"
        }
      ]
    }
  ]
}
```