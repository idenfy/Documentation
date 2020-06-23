## Table of contents
*   [Changelog](#changelog)
*   [Getting started](#getting-started)
*   [Callbacks](#callbacks)
*   [User events callbacks (optional)](#user-events-callbacks-optional)
*   [Customizing SDK V2 (optional)](#customizing-sdk-v2-optional)
*   [Customizing SDK V1 (optional)](#customizing-sdk-v1-optional)
*   [Customizing results callbacks V2 (optional)](#customizing-results-callbacks-v2-optional)
*   [Customizing results callbacks V1 (optional)](#customizing-results-callbacks-v1-optional)
*   [UI customization (optional)](#ui-customization)
*   [Samples](#samples)
*   [Advanced Liveness detection](#advanced-liveness-detection)

## Changelog
All updates will be written in this section.

Our SDK versioning conforms to [Semantic Versioning 2.0.0](https://semver.org/).

The structure of our changes follow practices from [keep a changelog](https://keepachangelog.com/en/1.0.0/).

## [2.4.0] - 2020-06-17
### Changed:
* Fixed constraints in initial view of V1 version, which resulted in insufficient padding on some devices.
* Improved speed of navigating after liveness preview.

## [2.3.0] - 2020-06-14
### Changed:
* Removed unnecessary empty spaces from Spanish locale strings.

## [2.2.1] - 2020-06-12
### Added:
* Added support for Gradle 4.0.0 plugin.
* Introduced identification instructions documentation.

## [2.1.0] - 2020-06-08
### Added:
* Added Swedish and Spanish localization.


### Added:
* Idenfy V2 SDK flow has been released!


## [2.0.0] - 2020-05-29

### Added:
* Idenfy V2 SDK flow has been released!


### Changed:
* Migrated to AndroidX dependencies. If your project still uses support library, you will need to enabled androidX support. More about AndroidX
* All layouts used in V1 have been migrated to AndroidX instead of support dependencies. If your project **overrides** layouts from V1, you should migrate them to AndroidX, otherwise runtime crashes will occur.
* Liveliness feature has been updated to V8! Please, update your current liveliness implementation as soon as possible. The only changes are related to UI customization. More about this here.
## Getting started

#### SDK version >=2.0.0:
The SDK supports API Level 16 and above.

Our current gradle configuration only supports AndroidX.

We suggest using Idenfy V2 SDK. It offers cleaner UI/UX and more customization options. All future improvements will be added only to V2 version.

#### SDK version <2.0.0:
The SDK supports API Level 15 and above.

Our current gradle configuration supports 

`targetSdkVersion = 28`

`compileSdkVersion = 28`

`buildToolsVersion '28.1.1'`

### 1. Obtaining token

SDK requires token for starting initialization. [Token generation guide](https://github.com/idenfy/Documentation/blob/master/pages/GeneratingIdentificationToken.md)

### 2. Adding the SDK dependency

In the root level (project module) gradle add following implementation:

```gradle
repositories {
    maven {
        url  "https://dl.bintray.com/idenfy/idenfy"
  }
}
```
In the app level gradle add following implementation:
```gradle
repositories {
    dependencies {  
      implementation 'idenfySdk:com.idenfy.idenfySdk:+' 
    }
}
```
*Note: All new versions will support backwards compatibility.
### 3. Enabling Java 8 support

It is required to enable Java 8 support, if it was already not provided:
```gradle
 compileOptions {
        targetCompatibility 1.8
        sourceCompatibility 1.8
    }
```

### 4. Configuring SDK

It is required to provide following configuration:
#### V2
##### Java
```java
IdenfySettingsV2 idenfySettingsV2 = new IdenfySettingsV2.IdenfyBuilderV2()
                .withAuthToken("AUTH_TOKEN")
                .build();
```

#### V1
##### Java
```java
IdenfySettings idenfySettings = new IdenfySettings.IdenfyBuilder()
                .withAuthToken("AUTH_TOKEN")
                .build();
```
### 5. Presenting Activity

Instance of IdenfyController is required for starting a flow.
#### V2
##### Java
```java
   IdenfyController.getInstance().startActivityForResultV2(context, IdenfyController.IDENFY_REQUEST_CODE, idenfySettingsV2);
   //context must be of an activity type.
```
#### V1
##### Java
```java
   IdenfyController.getInstance().startActivityForResult(context, IdenfyController.IDENFY_REQUEST_CODE, idenfySettings);
   //context must be of an activity type.
```
## Callbacks

SDK provides following callbacks: onSuccess, onError and onUserExit.

It is required to override onActivityResult for receiving responses.

#### V1, V2
##### Java
```java
    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if (requestCode == IdenfyController.IDENFY_REQUEST_CODE) {

            if (resultCode == IdenfyController.AUTHENTICATION_RESULT_CODE) {
                AuthenticationResultResponse authenticationResultResponse = data.getParcelableExtra(IdenfyController.ON_AUTHENTICATION_RESULT);
                //user proceeded identification. Here you would typically check for Identification status to determine your application flow.
                switch (authenticationResultResponse.getIdenfyIdentificationStatus()){
                    case SUSPECTED:
                        //user was suspected, while performing identification.
                        break;
                    case DENIED:
                        //identification was denied.
                        break;
                    case APPROVED:
                        //identification was approved.
                        break;
                    case REVIEWING:
                        //identification is still under review.
                        break;
                }
            } else if (resultCode == IdenfyController.ERROR_CODE) {
                IdenfyErrorResponse idenfyErrorResponse = data.getParcelableExtra(IdenfyController.ON_ERROR);
               //Error occurred within identification process.
            } else if (resultCode == IdenfyController.USER_EXIT_CODE) {
               //User exited the SDK without completing identification process.
            }
            
        }
    }
```
[Additional information about error responses](https://github.com/idenfy/Documentation/blob/master/pages/StandardErrorMessages.md)

## User events callbacks (optional)

SDK provides callbacks from the user flow throughout identification process.
Results will be delivered while identification process is occurring and application is presenting views of the SDK.

 ### 1. Declare a class for receiving events

Declare a class that implements IdenfyUserFlowHandler to call your backend service, log events or apply changes.
#### V1, V2
##### Java
```java
public class IdenfyUserFlowCallbacksHandler implements IdenfyUserFlowHandler {

    /**
     * @param documentType Selected document type.
     */
    @Override
    public void onDocumentSelected(@NotNull String documentType) {
        Log.d("userFlowCallback", documentType);
        setDocumentType(documentType);
    }

    /**
     * An example of a network request to save successful event.
     */
    public void setDocumentType(String documentType) {
        //...
        retrofit2.Call<DemoResponse> demoRequest =
                RetrofitFactory.create().demoRequest();
        demoRequest.enqueue(new Callback<DemoResponse>() {

            @Override
            public void onResponse(retrofit2.Call<DemoResponse> call, Response<DemoResponse> response) {
            }

            @Override
            public void onFailure(retrofit2.Call<DemoResponse> call, Throwable t) {
            }
        });
    }

    /**
     * @param issuingCountryCode Selected issuingCountryCode.
     */
    @Override
    public void onCountrySelected(@NotNull String issuingCountryCode) {
        Log.d("userFlowCallback", issuingCountryCode);

    }

    /**
     * @param photosUploaded indicates that photos have been uploaded.
     */
    @Override
    public void onPhotosUploaded(boolean photosUploaded) {
        Log.d("userFlowCallbacks", String.valueOf(photosUploaded));
    }

    /**
     * @param processingStarted indicates that processing has started.
     */
    @Override
    public void onProcessingStarted(boolean processingStarted) {
        Log.d("userFlowCallback", String.valueOf(processingStarted));

    }
}
```
 ### 2. Configure application class

Set IdenfyUserFlowController to reference idenfyUserFlowCallbacksHandler in the application class.

##### Java
```java
public class TestApplication extends Application {
    @Override
    public void onCreate() {
        super.onCreate();
        IdenfyUserFlowCallbacksHandler idenfyUserFlowCallbacksHandler =
                new IdenfyUserFlowCallbacksHandler();
        IdenfyUserFlowController.setIdenfyUserFlowHandler(idenfyUserFlowCallbacksHandler);
    }
}
```
*Note: it is required to set callbacks handler in the **application** class to ensure that listener will be set again after application process has stopped.

## Customizing SDK V2 (optional)
SDK provides various options for changing identification flow. All requirements can be specified with IdenfyBuilderV2().

### 1. Localization
By default SDK provides following translations:

- English (en) GB
- Polish (pl) PL
- Russian (ru) RU
- Lithuanian (lt) LT
- German (de) DE
- French (fr) FR
- Italian (it) IT
- Latvian (lv) LV
- Romanian (ro) RO
- Swedish (sv) SV
- Spanish (es) ES

All keys are located [here](https://github.com/idenfy/Documentation/blob/master/resources/sdk/android/localization/).  You can supply partial translations, meaning if you don't include a translation to particular key, then our SDK will use default keys. In order to see changes add particular xml to your app target or copy only specific keys in your strings.xml and changes will take effect.

### 2. Forcing specific language
The default language of SDK is selected by the language configurations of the **device**. In order to force particular locale use:
##### Java
```java
    IdenfySettingsV2.IdenfyBuilderV2()
    .withSelectedLocale(IdenfyLocaleEnum.EN)
    ...
```

## Customizing SDK V1 (optional)

 SDK provides various options for changing identification flow. All requirements can be specified with IdenfyBuilder().
 
 ### 1. Removing initial Fragment

If default document country was selected during **token generation** the terms of services and country information View can be removed.
##### Java
```java
    IdenfySettings.IdenfyBuilder()
    .withPresentInitialView(false)
    ...
```

### 2. Setting custom results view

If results view UI is not suitable for your design we provide customization. We provide full xml file of results view.
##### Java
```java
    IdenfySettings.IdenfyBuilder()
    .withCustomResultsView(true)
    ...
```

### 3. Custom locale

 By default SDK provides following translations:

- English (en) GB
- Polish (pl) PL
- Russian (ru) RU
- Lithuanian (lt) LT
- German (de) DE
- French (fr) FR
- Italian (it) IT
- Swedish (sv) SV
- Spanish (es) ES

The default language of SDK is selected by the language configurations of the **device**. In order to setup custom localization the following method must be called:
##### Java
```java
    IdenfySettings.IdenfyBuilder()
    .withCustomSelectedLocale("locale")
    ...
```

## Customizing results callbacks V2 (optional)

Identification results window provides sets of option to customize identification results look and interaction. For instance, if you have implemented manual callback it might be wise to disable **DENIED** or **APPROVED** views for better UI/UX. 

For handling identification status yourself, **immediate redirect feature** can be applied. After enabling immediate redirect the following results will take place:
### APPROVED screen will not be visible
If identification was approved, user will not see successful screen. SDK will be closed while displaying a loading screen. That way you can show a success screen yourself at particular time.
### DENIED screen will not be visible
Denied screen will not be visible. SDK will be closed while displaying a loading screen. That way you can display a error screen yourself at particular time.

*Note: For enabling immediate redirect contact support@idenfy.com.




## Customizing results callbacks V1 (optional)

SDK provides set of options to customize results view and callbacks handling.

*Note: callbacks will continue to occur as usual in onActivityResult().

 ### 1. Create the IdenfyIdentificationResultsSettings class

Create the IdenfyIdentificationResultsSettings instance and apply settings:

```java
IdenfyIdentificationResultsSettings idenfyIdentificationResultsSettings = new IdenfyIdentificationResultsSettings();

idenfyIdentificationResultsSettings.setSuccessResultsViewVisible(true);

idenfyIdentificationResultsSettings.setErrorResultsViewVisible(false);

idenfyIdentificationResultsSettings.setRetryErrorResultsViewVisible(true);

idenfyIdentificationResultsSettings.setRetryingIdentificationAvailable(false);
```

|Method name              |Description                     |
|-------------------|-------------------------------|
|`setSuccessResultsViewVisible(true)`   |Sets success results view visible, before providing callback. Default is true.                        |
|`setErrorResultsViewVisible(false)`|Sets general error results view visible, before providing callback. Default is true.                   |
|`setRetryErrorResultsViewVisible(true)`  |Sets retrying identification results view visible. Default is true.                 |
|`setRetryingIdentificationAvailable(true)`  |Enables identification retrying after unsuccessful identification.                 |

 ### 2. Update IdenfyBuilder

Update idenfyBuilder to apply changes:
##### Java
```java
    IdenfySettings.IdenfyBuilder()
    .withCustomIdentificationResultsSettings(idenfyIdentificationResultsSettings)
    ...
```

## UI customization

Please take a look at UI customization page:
[UI customization guidelines](https://github.com/idenfy/Documentation/blob/master/pages/AndroidUICustomization.md)

## Samples
### Sample SDK code
A following code demonstrates possible iDenfySDK configuration with applied settings:

#### V2
##### Java
```java
    private void initializeIDenfySDK(String authToken) 
    {
        IdenfySettingsV2 idenfySettingsV2 = new IdenfySettingsV2.IdenfyBuilderV2()
                .withAuthToken(authToken)
                .build();

        IdenfyController.getInstance().startActivityForResultV2(this, IdenfyController.IDENFY_REQUEST_CODE, idenfySettingsV2);
    }

    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if (requestCode == IdenfyController.IDENFY_REQUEST_CODE) {

            if (resultCode == IdenfyController.AUTHENTICATION_RESULT_CODE) {
                AuthenticationResultResponse authenticationResultResponse = data.getParcelableExtra(IdenfyController.ON_AUTHENTICATION_RESULT;
                Log.d("iDenfySDK", authenticationResultResponse.toString());
            } else if (resultCode == IdenfyController.ERROR_CODE) {
                IdenfyErrorResponse idenfyErrorResponse = data.getParcelableExtra(IdenfyController.ON_ERROR);
                Log.d("iDenfySDK", idenfyErrorResponse.toString());
            } else if (resultCode == IdenfyController.USER_EXIT_CODE) {
                Log.d("iDenfySDK", "user exits");
            }

        }
        
    }
```


#### V1
##### Java
```java
    private void initializeIDenfySDK(String authToken) 
    {

        IdenfyUISettings idenfyUISettings = new IdenfyUISettings.IdenfyUIBuilder()
                .withCustomLoadingView(R.drawable.custom_progress_bar)
                .build();

        IdenfyIdentificationResultsSettings idenfyIdentificationResultsSettings = new IdenfyIdentificationResultsSettings();
        idenfyIdentificationResultsSettings.setSuccessResultsViewVisible(true);
        idenfyIdentificationResultsSettings.setErrorResultsViewVisible(false);
        idenfyIdentificationResultsSettings.setRetryErrorResultsViewVisible(true);
        idenfyIdentificationResultsSettings.setRetryingIdentificationAvailable(false);

        IdenfySettings idenfySettings = new IdenfySettings.IdenfyBuilder()
                .withAuthToken(authToken)
                .withUISettings(idenfyUISettings)
                .withCustomSelectedLocale("en")
                .withCustomIdentificationResultsSettings(idenfyIdentificationResultsSettings)
                .withCustomResultsView(true)
                .build();

        IdenfyController.getInstance().startActivityForResult(this, IdenfyController.IDENFY_REQUEST_CODE, idenfySettings);
    }

    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if (requestCode == IdenfyController.IDENFY_REQUEST_CODE) {

            if (resultCode == IdenfyController.AUTHENTICATION_RESULT_CODE) {
                AuthenticationResultResponse authenticationResultResponse = data.getParcelableExtra(IdenfyController.ON_AUTHENTICATION_RESULT;
                Log.d("iDenfySDK", authenticationResultResponse.toString());
            } else if (resultCode == IdenfyController.ERROR_CODE) {
                IdenfyErrorResponse idenfyErrorResponse = data.getParcelableExtra(IdenfyController.ON_ERROR);
                Log.d("iDenfySDK", idenfyErrorResponse.toString());
            } else if (resultCode == IdenfyController.USER_EXIT_CODE) {
                Log.d("iDenfySDK", "user exits");
            }

        }
        
    }
```

### SDK Integration tutorials
For more information visit [SDK integration tutorials](pages/tutorials/mobile-sdk-tutorials.md).


## Advanced Liveness detection

SDK provides advanced liveness recognition. Liveness recognition is attached as separate, optional module inside of the SDK. 

New major liveness version is released every 6-12 months. After major version release SDK must be updated also.

Attached liveness SDK will sync with **core** Idenfy SDK.

In the app level gradle add following implementation:
```gradle
repositories {
    dependencies {  
      implementation 'idenfySdk:com.idenfy.idenfySdk.idenfyliveness:+' 
    }
}
```
 
*Note: Contact support for enabling liveness feature.






