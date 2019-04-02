## Table of contents

*   [Getting started](#getting-started)
*   [Callbacks](#callbacks)
*   [User events callbacks](#user-events-callbacks)
*   [Customizing flow](#customizing-flow)
*   [Customizing results callbacks](#customizing-results-callbacks)
*   [UI Customization](#ui-customization)
*   [Advanced Liveness detection](#advanced-liveness-detection)

## Getting started
The SDK supports API Level 15 and above

Our current gradle configuration supports newest support library:

`targetSdkVersion = 27`

`compileSdkVersion = 27`

`buildToolsVersion '27.1.1'`


### 1. Obtaining token
SDK requires token for starting initialization. [Token generation guide](https://github.com/idenfy/Documentation/blob/master/pages/GeneratingIdentificationToken.md)

### 2. Adding the SDK dependency
In the root level (project module) gradle add following implementation:

```gradle
repositories {
  ...
  maven {
    url  "https://dl.bintray.com/idenfy/idenfy"
  }
}
```
In the app level gradle add following implementation:
```gradle
repositories {
  ...
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
### Java
```java
IdenfySettings idenfySettings = new IdenfySettings.IdenfyBuilder()
                .withAuthToken("AUTH_TOKEN")
                .build();
```


### 5. Presenting Activity
Instance of IdenfyController is required for starting a flow.

### Java
```java
   IdenfyController.getInstance().startActivityForResult(context, IdenfyController.IDENFY_REQUEST_CODE, idenfySettings);
   //context must be of a activity type
```
## Callbacks
SDK provides following callbacks: onSuccess, onError and onUserExit.

It is required to override onActivityResult for receiving responses.

After receiving **onSuccess or onError** response it is suggested to check status via API call.

### Java
```java
    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if (requestCode == IdenfyController.IDENFY_REQUEST_CODE) {

            if (resultCode == IdenfyController.AUTHENTICATION_RESULT_CODE) {
                AuthenticationResultResponse authenticationResultResponse = data.getParcelableExtra(IdenfyController.ON_AUTHENTICATION_RESULT);
                //user procceeded identification. Here you would typically check for Identification status and check response using API call
            } else if (resultCode == IdenfyController.ERROR_CODE) {
                IdenfyErrorResponse idenfyErrorResponse = data.getParcelableExtra(IdenfyController.ON_ERROR);
                //Error response
            } else if (resultCode == IdenfyController.USER_EXIT_CODE) {
                //User exited the SDK
            }
            
        }
    }
```


[Additional information about callbacks](https://github.com/idenfy/Documentation/blob/master/pages/StandardErrorMessages.md)

## User events callbacks

SDK provides callbacks from the user flow throughout identification process.
Results will be delivered while identification process is occurring and application is presenting views of the SDK.

 ### 1. Declare a class for receiving events

Declare a class that implements IdenfyUserFlowHandler to call your backend service, log events or apply changes.

```java
public class IdenfyUserFlowCallbacksHandler implements IdenfyUserFlowHandler {

    /**
     * @param documentType Selected document type
     */
    @Override
    public void onDocumentSelected(@NotNull String documentType) {
        Log.d("userFlowCallback", documentType);
        setDocumentType(documentType);
    }

    /**
     * an example of a network request to indicate event success
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
     * @param issuingCountryCode Selected issuingCountryCode
     */
    @Override
    public void onCountrySelected(@NotNull String issuingCountryCode) {
        Log.d("userFlowCallback", issuingCountryCode);

    }

    /**
     * @param photosUploaded indicated that photos have been uploaded
     */
    @Override
    public void onPhotosUploaded(boolean photosUploaded) {
        Log.d("userFlowCallbacks", String.valueOf(photosUploaded));
    }

    /**
     * @param processingStarted indicates that processing has started
     */
    @Override
    public void onProcessingStarted(boolean processingStarted) {
        Log.d("userFlowCallback", String.valueOf(processingStarted));

    }
}
```
 ### 2. Configure application class
Set IdenfyUserFlowController to reference idenfyUserFlowCallbacksHandler in the application class.

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
*Note it is required to set callbacks handler in the **application** class to ensure that listener will be set again after application process has stopped.


## Customizing flow
 SDK provides various options for changing identification flow. All requirements can be specified inside of IdenfyBuilder()
 
 *Note: SDK provides Builder pattern to improve code testibility and maitanance. Equivalently setters can also be used.
 
 ### 1. Removing initial Fragment

If default document country was selected during **token generation** the terms of services and country information View can be removed.
```java
   IdenfySettings.IdenfyBuilder()
    .withPresentInitialView(false)
    ...
```

### 2. Setting custom results view

If results view UI is not suitable for your design we provide customization. We provide full xml file of results view
```java
   IdenfySettings.IdenfyBuilder()
    .withCustomResultsView(true)
    ...
```

### 3. Custom locale

 By default SDK provides following translations:

 - English (en) GB
 - Polish (es) PL
 - Russian (es) RU
 - Lithuanian (es) LT

The language of SDK is selected by the language configurations of the **device**. In order to setup custom localization the following method must be called
```java
   IdenfySettings.IdenfyBuilder()
    .withCustomSelectedLocale("locale")
    ...
```
## Customizing results callbacks

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
```java
   IdenfySettings.IdenfyBuilder()
    .withCustomIdentificationResultsSettings(idenfyIdentificationResultsSettings)
    ...
```
## UI Customization

SDK provides various ways of changing UI for better design integration.
 ### 1. UI settings

### Java
```java
IdenfyUISettings idenfyUISettings = new 
IdenfyUISettings.IdenfyUIBuilder()
    .build();
```
 ### 2. Customizable features
 Setting different progress indicator for custom layout
```java
IdenfyUISettings.IdenfyUIBuilder()
    withCustomLoadingView(Integer drawableId)
    ...
```
Removing actionBarLayout from UI. Helps to easier customize UI.
```java
IdenfyUISettings.IdenfyUIBuilder()
    withAppBarLayoutEnabled(boolean isActionBarEnabled)
    ...
```

For setting custom typeface.
```java
IdenfyUISettings.IdenfyUIBuilder()
    withTypefacePath(String pathOfTypeface)
    ...
```

 ## Advanced Liveness detection
SDK provides advanced liveness recognition. Liveness recognition is attached as separate, optional module inside of the SDK. 
 
Attached liveness SDK will sync with **core** Idenfy SDK.

In the app level gradle add following implementation:
```gradle
repositories {
  ...
  dependencies {  
      implementation 'idenfySdk:com.idenfy.idenfySdk.idenfyliveness:+' 
    }
}
```

In the root level (project module) gradle add following implementation:

```gradle
repositories {
    ...
    maven {
        url 'http://maven.facetec.com'
    }
}
```
 
*Note: Contact support for enabling liveness feature






