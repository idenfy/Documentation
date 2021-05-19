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

## [5.2.0] - 2020-05-18
### Added:
* NFC enhanced identity verification. More about it [here](#5-nfc-support)

## [5.1.1] - 2020-05-03
## Due to bintray sunsetting, we have migrated to the jitpack. If you face Gradle compile issues, switch to [jitpack integration](#2-adding-the-sdk-dependency)

## [5.1.1] - 2020-04-08
### Changed:
* Deprecated startActivityForResultV2 in favour of initializeIdenfySDKV2WithManual. The startActivityForResultV2 will be removed in the 6.0.0 version
* Min API set to 19. Starting version 6.0.0 min API will be set to 21.
* Lifecycle updates related to 3D liveness.


## [5.1.0] - 2020-04-07
### Added:
* Added a loading indicator after the user selected a document issuing country. This is due to recent updates, which now show available documents depending on issuing country selection. If your application overrides xml layouts of our SDK you should consider updating your **idenfy_item_document_issuing_country_selection_v2.xml** with Lottie animation of your preferred choice, so that the user would see a loading indicator, instead of occurring action delay. If you set issuing country during identification token generation via API or skip the document's issuing country step selection altogether, then **no UI changes** will be noticeable.
* Added option to **skip selfie capture** during 3D liveness identification. This feature was recently made the default choice for 3D liveness identification flow. So, updating the SDK you will see that the selfie step is **no longer present**. This functionality can be disabled if you like to keep the current flow or need more time updating your custom views contact techsupport@idenfy.com for disabling this feature.
### Changed:
* 3D Liveness version update.
* Removed the document capturing rectangle for the additional identification steps during the document photo capture step. The rectangle was confusing because some documents take a much larger size in comparison with the present capture frame size.
* Dependencies updated.


## [5.0.1] - 2020-03-08
### Changed:
* Upgraded CameraX versions and Gradle other dependencies.
* Fixed a state restoration/fragment's lifecycle issues in the documents selection view.
* Fixed permission alert dialog appearance issues.

## [5.0.0] - 2020-02-26
### Added:
* Major 3D liveness version upgrade from v8 to v9. Faster and more accurate 3D liveness. Starting with the 5.0.0 version liveness module is directly integrated into the SDK. More about this decision read [here](#advanced-liveness-detection).
* Fixed occurring runtime crashes on some devices when using 3D liveness with ID check.
* [SSL pinning support](#4-ssl-pinning-support).

### Changed:
* Core camera improvements.
* Identification recording duration increase.


## [4.2.0] - 2020-01-22
### Added:
* Added an option to set a custom additional step with the backend settings.

### Changed:
* Identification results loading screen for additional steps.

## [4.1.0] - 2021-01-05
### Changed:
* Moved camera permission request to the fragments, which require camera permission. This change provides better support for Android 11 permission changes.
* Deprecated startActivityForResultV2() in favour of initializeIdenfySDKV2WithManual(). The method startActivityForResultV2() will be removed in the next version.

### Added:
* Added new customization option - document's issuing country selection skipping with backend. More information [here](https://github.com/idenfy/Documentation/blob/master/pages/AndroidUICustomization.md#customization-with-skipping-views).
* Added new customization option - document's selection skipping with backend. More information [here](https://github.com/idenfy/Documentation/blob/master/pages/AndroidUICustomization.md#customization-with-skipping-views).
* Added new customization option - document's selection onboarding skipping with backend. More information [here](https://github.com/idenfy/Documentation/blob/master/pages/AndroidUICustomization.md#customization-with-skipping-views).

## [4.0.0] - 2020-12-11
### Changed:
* Renamed startWithManualResults to initializeIdenfySDKV2WithManual to match IOS SDK.
* Introduced additional WAITING status in the manualIdentificationStatus enum.
* Renamed layout idenfy_fragment_document_photo_result_v2.xml into the idenfy_fragment_document_photo_result_with_questions_v2.xml
* Renamed layout idenfy_fragment_face_photo_result_v2.xml into the idenfy_fragment_face_photo_result_with_questions_v2.xml
* Renamed layout idenfy_fragment_manual_reviewing_status_waiting_v2.xml into the idenfy_fragment_manual_reviewing_status_waiting_with_auto_results_steps_v2.xml

### Added:
* Added new UI elements in the document & selfie photo result screens. [Visual changes](https://github.com/idenfy/Documentation/blob/master/resources/sdk/android/changes/Android_SDK_4.0.0_PhotoResultsScreen.png).
* Removed terminate identification button and added new UI elements in the ManualResultsWaiting screen. [Visual changes](https://github.com/idenfy/Documentation/blob/master/resources/sdk/android/changes/Android_SDK_4.0.0_ManualWaitingResultsScreen.png).
* Added highly requested state restoration change. Previously the SDK would force a user to restart the identification flow as soon as the user went to the background. This behavior created inconveniences for the identification process. As a result, we redesigned state restoration.
The SDK no longer causes the identification restart as soon as the user goes to the background. The restart will only occur if the user spends **at least 5 minutes** while being in the background.

## [3.2.1] - 2020-11-17
### Added:
* Added support for the Bulgarian language.

## [3.2.0] - 2020-10-06
### Added:
* Added new ID-spoof detection support.
* Updated Liveness feature customization [options](https://github.com/idenfy/Documentation/blob/master/pages/AndroidUICustomization.md).

## [3.1.2] - 2020-10-05
### Added:
* Updated [cameraX](https://developer.android.com/training/camerax) library to the latest version.

## [3.1.1] - 2020-09-04
### Added:
* Started migration to [cameraX](https://developer.android.com/training/camerax) library. Idenfy contributed to an open-sourced cameraX project to make it the most stable camera solution on Android. If your app **overrides idenfy layouts**, make sure to include cameraX preview layout. All layouts are visible in Android Studio or [here](https://github.com/idenfy/Documentation/blob/master/resources/sdk/android/layouts/).
* A new error message for the user to notice if the identification process could not be completed.
### Changed:
* Fixed countries blacklist issue, which affected certain countries.
* Migrated camera session instructions to [ViewPager2](https://developer.android.com/jetpack/androidx/releases/viewpager2).

## [3.0.0] - 2020-08-20
### Added:
* Introduced manual identification flow!


## [2.8.0] - 2020-08-19
### Changed:
* Customization option to skip country selection.
* Colors customization option to set SDK wide color scheme with only a handful of changes.
* Renamed identification results assets names to better match the SDK statuses.

## [2.7.0] - 2020-08-05
### Changed:
* Removed instructions configuration from client customization in the V1 version. Read more about instructions [here](https://github.com/idenfy/Documentation/blob/master/pages/AndroidUICustomization.md#adding-instructions-in-camera-session).

## [2.6.0] - 2020-07-23
### Added:
* Network stability improved on poor network connections. Added better retry policy.

## [2.5.1] - 2020-07-01
### Added:
* Added support for proof of address.
### Changed:
* Changed utility bill strings to proof of address. If your app overrides strings, please update [keys](https://github.com/idenfy/Documentation/blob/master/resources/sdk/android/localization/).

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

The SDK supports API Level 16 and above.

Our current gradle configuration only supports AndroidX.

We suggest using Idenfy V2 SDK. It offers cleaner UI/UX and more customization options. All future improvements will be added only to V2 version.

### 1. Obtaining token

SDK requires token for starting initialization. [Token generation guide](https://github.com/idenfy/Documentation/blob/master/pages/GeneratingIdentificationToken.md)

### 2. Adding the SDK dependency

In the root level (project module) gradle add following implementation:

```gradle
repositories {
    maven { url 'https://jitpack.io' }
}
```
In the app level gradle add following implementation:
```gradle
repositories {
    dependencies {  
      implementation 'com.github.idenfy:sdk-api:5.2.0'
    }
}
```
*Note.
We suggest using a specific latest version unless you are not overriding any custom views or apply customization. This ensures that no **runtime crashes** will occur after automatic version upgrades. 

If you understand the disadvantages and still want to use the latest version integrate the SDK in the following way:
```gradle
repositories {
    dependencies {  
      implementation 'com.github.idenfy:sdk-api:+'
    }
}
```
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
#### initializeIdenfySDKV2WithManual
##### Java
```java
IdenfySettingsV2 idenfySettingsV2 = new IdenfySettingsV2.IdenfyBuilderV2()
                .withAuthToken("AUTH_TOKEN")
                .build();
```

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

***Note**: We recommend implementing the initialization of the SDK with the initializeIdenfySDKV2WithManual(). 
The regular V2 initialization will be removed in the future, while initialization with the manual identification results provides easier integration, existing **V2 version** customization options and similar callbacks handling to our [iFrame solution](https://github.com/idenfy/Documentation/blob/master/pages/ClientRedirectToWebUiIframe.md). 

### 5. Presenting Activity

Instance of IdenfyController is required for starting a flow.

**Recommended approach**
#### initializeIdenfySDKV2WithManual
##### Java
```java
IdenfyController.getInstance().initializeIdenfySDKV2WithManual(context,
                IdenfyController.IDENFY_REQUEST_CODE,
                idenfySettingsV2);
    //context must be of an activity type.
```

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

It is required to override onActivityResult for receiving responses.

#### initializeIdenfySDKV2WithManual
### Java
```java
    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if (requestCode == IdenfyController.IDENFY_REQUEST_CODE) {
            if (resultCode == IdenfyController.IDENFY_IDENTIFICATION_RESULT_CODE) {
                IdenfyIdentificationResult idenfyIdentificationResult = data.getParcelableExtra(IdenfyController.IDENFY_IDENTIFICATION_RESULT);
                if (idenfyIdentificationResult != null) {
                    switch (idenfyIdentificationResult.getAutoIdentificationStatus()) {

                        case APPROVED:
                            break;
                        case FAILED:
                            break;
                        case UNVERIFIED:
                            break;
                    }

                    switch (idenfyIdentificationResult.getManualIdentificationStatus()) {
                        case APPROVED:
                            break;
                        case FAILED:
                            break;
                        case INACTIVE:
                            break;
                    }
                }
                Toast.makeText(this, idenfyIdentificationResult.toString(), Toast.LENGTH_LONG).show();
            }
        }
    }
```

Information about the IdenfyIdentificationResult **autoIdentificationStatus** statuses:

|Name            |Description
|-------------------|------------------------------------
|`APPROVED`   |The user completed an identification flow and the identification status, provided by an automated platform, is APPROVED.
|`FAILED`|The user completed an identification flow and the identification status, provided by an automated platform, is FAILED.
|`UNVERIFIED`   |The user did not complete an identification flow and the identification status, provided by an automated platform, is UNVERIFIED. 

Information about the IdenfyIdentificationResult **manualIdentificationStatus** statuses:

|Name            |Description
|-------------------|------------------------------------
|`APPROVED`   |The user completed an identification flow and was verified manually while waiting for the manual verification results in the iDenfy SDK. The identification status, provided by a manual review, is APPROVED.
|`FAILED`|The user completed an identification flow and was verified manually while waiting for the manual verification results in the iDenfy SDK. The identification status, provided by a manual review, is FAILED.
|`WAITING`|The user completed an identification flow and started waiting for the manual verification results in the iDenfy SDK. Then he/she decided to stop waiting and pressed a "BACK TO ACCOUNT" button. The manual identification review is **still ongoing**.
|`INACTIVE`   |The user was only verified by an automated platform, not by a manual reviewer. The identification performed by the user can still be verified by the manual review if your system uses the manual verification service.

*Note
The manualIdentificationStatus status always returns INACTIVE status, unless your system implements manual identification callback, but does not create **a separate waiting screen** for indicating about the ongoing manual identity verification process.
For better customization we suggest using the [immediate redirect feature ](#customizing-results-callbacks-v2-optional). As a result, the user will not see an automatic identification status, provided by iDenfy service. The SDK will be closed while showing loading indicators.

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
##### Kotlin
```kotlin
    override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
        super.onActivityResult(requestCode, resultCode, data)
        if (requestCode == IdenfyController.IDENFY_REQUEST_CODE) {
            if (resultCode == IdenfyController.IDENFY_IDENTIFICATION_RESULT_CODE) {
                val idenfyIdentificationResult: IdenfyIdentificationResult =
                    data!!.getParcelableExtra(IdenfyController.IDENFY_IDENTIFICATION_RESULT)

                when (idenfyIdentificationResult.autoIdentificationStatus) {
                    AutoIdentificationStatus.APPROVED -> {
                    }
                    AutoIdentificationStatus.FAILED -> {
                    }
                    AutoIdentificationStatus.UNVERIFIED -> {
                    }
                }
                
                when (idenfyIdentificationResult.manualIdentificationStatus) {
                    ManualIdentificationStatus.APPROVED -> {
                    }
                    ManualIdentificationStatus.FAILED -> {
                    }
                    ManualIdentificationStatus.WAITING -> {
                    }
                    ManualIdentificationStatus.INACTIVE -> {
                    }
                }

                Toast.makeText(this, idenfyIdentificationResult.toString(), Toast.LENGTH_LONG)
                    .show()
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
#### V1, V2, initializeIdenfySDKV2WithManual
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
### 3. User flow customization
#### * Language selection skipping
The SDK provides an option to skip **document's issuing country** selection. If the document's issuing country is set in the [identification token generation process](https://github.com/idenfy/Documentation/blob/master/pages/GeneratingIdentificationToken.md) it might be more UX friendlier to skip issuing country selection and navigate the user to document selection screen. 
##### Java
```java
    IdenfySettingsV2.IdenfyBuilderV2()
    .withAuthToken(authToken)
    .withDocumentIssuingCountrySkipped()
    ...
    .build()
```
*NOTE, make sure that issuing country is indeed set, when generating an identification token. If issuing country is not set, SDK will behave in a default way - it will navigate user into document issuing country selection screen.

### 4. SSL pinning support
By default, the SDK does not utilize SSL pinning as suggested by the **AWS services**.
If you however need this option, you can enable SSL pinning.
Our SSL pinning implementation does follow the [AWS recommendations](https://aws.amazon.com/premiumsupport/knowledge-center/pin-application-acm-certificate/) and we utilize pinning for the Root certificates. They are valid for more than 5+ years. 

However, during this timeframe, major changes can occur and we might be forced to change SSL pinning. Such changes will be notified at least 1 month prior. 

This is why we strongly encourage you to enable this feature only if you are planning to **actively update the SDK**.

##### Kotlin
```kotlin
    val idenfySettingsV2 = IdenfyBuilderV2()
        .withAuthToken(authToken)
        .withSSLPinning(true)
        ...
        .build()
    ...
```
### 5. NFC support
The SDK provides NFC enhanced identity verification. For more integration details and potential advantages contact techsupport@idenfy.com. 
After NFC is enabled for your client settings, **no additions** integrations are required on the SDK side.

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

#### initializeIdenfySDKV2WithManual
##### Java
```java
    private void initializeIDenfySDK(String authToken) 
    {
        IdenfySettingsV2 idenfySettingsV2 = new IdenfySettingsV2.IdenfyBuilderV2()
                .withAuthToken(authToken)
                .build();

        IdenfyController.getInstance().initializeIdenfySDKV2WithManual(this, IdenfyController.IDENFY_REQUEST_CODE, idenfySettingsV2);
    }

    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if (requestCode == IdenfyController.IDENFY_REQUEST_CODE) {
            if (resultCode == IdenfyController.IDENFY_IDENTIFICATION_RESULT_CODE) {
                IdenfyIdentificationResult idenfyIdentificationResult = data.getParcelableExtra(IdenfyController.IDENFY_IDENTIFICATION_RESULT);
                if (idenfyIdentificationResult != null) {
                    switch (idenfyIdentificationResult.getAutoIdentificationStatus()) {

                        case APPROVED:
                            break;
                        case FAILED:
                            break;
                        case UNVERIFIED:
                            break;
                    }
                    
                    switch (idenfyIdentificationResult.getManualIdentificationStatus()) {
                        case APPROVED:
                            break;
                        case FAILED:
                            break;
                        case WAITING:
                            break;
                        case INACTIVE:
                            break;
                    }
                }
                Toast.makeText(this, idenfyIdentificationResult.toString(), Toast.LENGTH_LONG).show();
            }
        }
    }
```

##### Kotlin
```Kotlin
    private fun initializeIDenfySDK(authToken: String) 
    {
        val idenfyUISettingsV2 = IdenfyUIBuilderV2()
            .withInstructions(true)
            .build()
        val idenfySettingsV2 = IdenfyBuilderV2()
            .withAuthToken(authToken)
            .withIdenfyUISettingsV2(idenfyUISettingsV2)
            .build()
        IdenfyController.getInstance().initializeIdenfySDKV2WithManual(
            this,
            IdenfyController.IDENFY_REQUEST_CODE,
            idenfySettingsV2
    }

    override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
        super.onActivityResult(requestCode, resultCode, data)
        if (requestCode == IdenfyController.IDENFY_REQUEST_CODE) {
            if (resultCode == IdenfyController.IDENFY_IDENTIFICATION_RESULT_CODE) {
                val idenfyIdentificationResult: IdenfyIdentificationResult =
                    data!!.getParcelableExtra(IdenfyController.IDENFY_IDENTIFICATION_RESULT)

                when (idenfyIdentificationResult.autoIdentificationStatus) {
                    AutoIdentificationStatus.APPROVED -> {
                    }
                    AutoIdentificationStatus.FAILED -> {
                    }
                    AutoIdentificationStatus.UNVERIFIED -> {
                    }
                }
                
                when (idenfyIdentificationResult.manualIdentificationStatus) {
                    ManualIdentificationStatus.APPROVED -> {
                    }
                    ManualIdentificationStatus.FAILED -> {
                    }
                    ManualIdentificationStatus.WAITING -> {
                    }
                    ManualIdentificationStatus.INACTIVE -> {
                    }
                }

                Toast.makeText(this, idenfyIdentificationResult.toString(), Toast.LENGTH_LONG)
                    .show()
            }
        }
    }
```


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
For more information visit [SDK integration tutorials](https://github.com/idenfy/Documentation/blob/master/pages/tutorials/mobile-sdk-tutorials.md).


## Advanced Liveness detection

SDK provides advanced liveness recognition.

The liveness feature is not optimized for tablets. As a result, identification performed via tablet will be automatically classified as **denied**.

The new major liveness version is released every 6-12 months. Your app must update the liveness module after every major release. If SDK is not updated, it can lead to the **runtime crashes**.

Starting version 5.0.0 3D module is directly integrated inside of the main SDK. We suggest including **additional liveness module**, because it will make migration easier in the future. 

The main condition is to use **same version** as the core liveness. Using different versions can lead to crashes, additional unnecessary application size increases. 

Include the 3D liveness module:

```gradle
repositories {
    dependencies {  
      implementation 'com.github.idenfy:sdk-liveness:5.2.0'
    }
}
```
We performed such decision, because of the size reduction of the native code (from 8 Mb to ~3.5 Mb). 

Also, the previous liveness version was included with **compileOnly** Gradle annotation. This annotation could cause potential issues if migration would be done incorrectly on your side e.g. updating core SDK to 5.0.0, but keeping the liveness module to 4.2.0.

Furthermore, it was difficult to add 3D liveness, if your previous SDK used regular SDK because 3D liveness configurations are received via API, so your application would require **force updates** to make sure that all users have an additional 3D liveness module.

Currently, our team is looking closely at [gradle feature variants](https://docs.gradle.org/current/userguide/feature_variants.html). It did not cover all of our cases, but we think that after upcoming updates it will be a viable solution for modularizing our SDK's modules distribution.

*Note: Contact support for enabling the 3D liveness feature.







