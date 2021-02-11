## Table of contents
*   [Changelog](#changelog)
*   [Getting started](#getting-started)
*   [Callbacks](#callbacks)
*   [Customizing SDK V2 (optional)](#customizing-sdk-v2-optional)
*   [Customizing SDK V1 (optional)](#customizing-sdk-v1-optional)
*   [Customizing results callbacks V2 (optional)](#customizing-results-callbacks-v2-optional)
*   [Customizing results callbacks V1 (optional)](#customizing-results-callbacks-v1-optional)
*   [UI customization](#ui-customization)
*   [Samples](#samples)
*   [Advanced Liveness detection](#advanced-liveness-detection)


## Changelog
All updates will be written in this section.

Our SDK versioning conforms to [Semantic Versioning 2.0.0](https://semver.org/).

The structure of our changes follow practices from [keep a changelog](https://keepachangelog.com/en/1.0.0/).

## [6.0.0] - 2020-02-11
### Added:
* [SSL pinning support](#customizing-sdk-v2-optional).
* Major 3D liveness version upgrade from v8 to v9. Faster and more accurate 3D liveness. 

### Changed:
* Changed 3D liveness localization strings names from Zoom.strings to the **FaceTec.strings**. In order to support multilanguages in the 3D liveness you have to override those strings.
* Made changes for [custom identification results ViewController customizations](https://github.com/idenfy/Documentation/blob/master/pages/IOSUICustomization.md#customization-by-providing-a-CustomWaitingViewController).
* Improved identifications recording. Videos will be longer. 


## [5.3.0] - 2020-01-29
### Added:
* Added an option to set [a custom identification results ViewController](https://github.com/idenfy/Documentation/blob/master/pages/IOSUICustomization.md#customization-by-providing-a-CustomWaitingViewController).
* More document selection customization improvements.

## [5.2.0] - 2020-01-22
### Added:
* Added an option to set a custom additional step with the backend settings.

### Changed:
* Identification results loading screen for additional steps.

## [5.1.0] - 2020-01-05
### Added:
* Added new customization option - document's issuing country selection skipping with backend. More information [here](https://github.com/idenfy/Documentation/blob/master/pages/IOSUICustomization.md#customization-with-skipping-views).
* Added new customization option - document's selection skipping with backend. More information [here](https://github.com/idenfy/Documentation/blob/master/pages/IOSUICustomization.md#customization-with-skipping-views).
* Added new customization option - document's selection onboarding skipping with backend. More information [here](https://github.com/idenfy/Documentation/blob/master/pages/IOSUICustomization.md#customization-with-skipping-views).

### Changed:
* Miscellaneous bug fixes (UI).

## [5.0.0] - 2020-12-11
### Changed:
* Renamed initializeIdenfySDKV2WithManualWithIdenfySettingsV2 to initializeIdenfySDKV2WithManual to match Android SDK.
* Introduced additional WAITING status in the manualIdentificationStatus enum.
* Removed initializeIdenfySDKV2(), because initializeIdenfySDKV2WithManual provides same functionality.


### Added:
* Added new UI elements in the document & selfie photo result screens. [Visual changes](https://github.com/idenfy/Documentation/blob/master/resources/sdk/ios/changes/IOS_SDK_5.0.0_PhotoResultsScreen.png).
* Removed terminate identification button and added new UI elements in the ManualResultsWaiting screen. [Visual changes](https://github.com/idenfy/Documentation/blob/master/resources/sdk/ios/changes/IOS_SDK_5.0.0_ManualWaitingResultsScreen.png).
* Added highly requested state restoration change. Previously the SDK would force a user to restart the identification flow as soon as the user went to the background. This behavior created inconveniences for the identification process. As a result, we redesigned state restoration.
The SDK no longer causes the identification restart as soon as the user goes to the background. The restart will only occur if the user spends **at least 5 minutes** while being in the background.
* Added a new [V2 customization option](https://github.com/idenfy/Documentation/blob/master/pages/IOSUICustomization.md#customization-by-providing-custom-idenfyviewsv2-class). This customization is a significant improvement from the previous solution.

## [4.3.1] - 2020-11-17
### Added:
* Added support for the Bulgarian language.
* Reduced memory footprint.

## [4.3.0] - 2020-10-07
### Added:
* Updated Liveness feature customization [options](https://github.com/idenfy/Documentation/blob/master/pages/IOSUICustomization.md).
* Improved network requests handling on poor network conditions, specifically short connectivity disappearance.

## [4.2.0] - 2020-09-21
### Added:
* Added new ID-spoof detection support.

### Changed:
* Significantly improved 3D-liveness recognition accuracy.
* Improved 3D-liveness UX flow. Added explanations when the liveness check performed incorrectly.


## [4.1.0] - 2020-09-04
### Added:
* Added a new screen if the user has disabled camera permissions. It provides information about camera permission and why iDenfy needs it.
* Added Objective-C support for the V2 SDK version.
* Added additional error message for developers, which will be triggered if the [liveness feature](#advanced-liveness-detection) is enabled, but the wrong SDK is installed.
* Document confirmation screen is enabled by default now.

### Changed:
* Migrated to Swift 5.0. Use Xcode version >=11.
* Locale changes within the app will also affect the locale of the [liveness feature](#advanced-liveness-detection).

## [4.0.0] - 2020-08-20
### Added:
* Introduced manual identification flow!

## [3.4.0] - 2020-08-18
### Added:
* Better network requests handling on poor network conditions.
* Customization option to skip country selection.
* Colors customization option to set SDK wide color scheme with only a handful of changes.
* Renamed identification results assets names to better match the SDK statuses.


## [2.1.0] - 2020-08-03
### Changed:
* Migrated to updated liveness version in SDK versions lower than 3.00. A brand new flow with better UX for performing 3D liveness verification. Read more about liveness versioning and [updates frequency](https://github.com/idenfy/Documentation/blob/master/pages/ios-sdk.md#advanced-liveness-detection).
*Note: this update was already present in the SDK, starting with version 3.0.0.

## [3.3.0] - 2020-07-01
### Added:
* Added support for proof of address.
### Changed:
* Changed utility bill strings to proof of address. If your app overrides strings, please update [keys](https://github.com/idenfy/Documentation/blob/master/resources/sdk/ios/localization/).

## [3.2.3] - 2020-06-17
### Changed:
* Fixed translations in Polish language.

## [3.2.2] - 2020-06-16
### Changed:
* Fixed issues with translations in V1 Alert of initial view.

## [3.2.1] - 2020-06-12
### Added:
* Added full UI customization documentation.
* Introduced identification instructions documentation.
* Added manual integration guide.

## [3.1.0] - 2020-06-08
### Added:
* Added Swedish and Spanish localization.

## [3.0.0] - 2020-05-29

### Added:
* Idenfy V2 SDK flow has been released!


### Changed:
* Liveliness feature has been updated to V8! Please, update your current liveliness implementation as soon as possible. The only changes are related to UI customization. More about this here.

## [2.0.0] - 2020-05-04

### Added:
* Support for French, Italian and German languages. 

### Changed:
* Removed previously deprecated UIWebView references from Storyboard. If custom storyboard was used for initializing SDK it will cause a **runtime crash**, because of UIWebView presence in the **FaceCameraViewController**. After upgrading the SDK, remove UIWebView reference in the **FaceCameraViewController**. 

    No changes are needed if UIWebView is already removed from custom Idenfy.storyboard.

* Renamed withCustomsStoryboard -> withCustomLocalStoryboard initialization method.

## Getting started

* The minimum version of IOS, supported by the SDK is 9.0.

### 1. Obtaining token

SDK requires token for starting initialization. [Token generation guide](https://github.com/idenfy/Documentation/blob/master/pages/GeneratingIdentificationToken.md)

### 2. Providing permissions

 `NSCameraUsageDescription' must be provided in the application's 'Info.plist' file:

```xml
<key>NSCameraUsageDescription</key>
<string>Required for document and facial capture</string>
```
### 3. Adding the SDK dependency
#### CocoaPods
```ruby
pod 'iDenfySDK', '5.4.0'
```
*Note.
We suggest using a specific latest version unless you are not overriding any custom views or apply customization. This ensures that no **runtime crashes** will occur after automatic version upgrades. 

If you understand the disadvantages and still want to use the latest version integrate the SDK in the following way:
```ruby
pod 'iDenfySDK'
```

#### Manual
##### 1. Download iDenfySDK
[Download](https://s3-eu-west-1.amazonaws.com/sdk.builds/ios-sdk/4.1.0/iDenfySDK.zip) latest iDenfySDK builds.
##### 2. Include required modules
##### 2.1 With liveness module
If you are using [Advanced Liveness detection](#advanced-liveness-detection) copy all frameworks from IdenfyLiveness folder into your app target folder.

*Note: In order to use localized version of liveness feature add Zoom.strings to your app module.

Strings are located in  **../iDenfySDK/IdenfyAssets/IdenfyStrings**

##### 2.2 With regular iDenfySDK
Otherwise copy all frameworks from IdenfySDK folder into your app target folder.
##### 3. Embed & Sign
Embed & Sign included frameworks.

<kbd><img src="https://github.com/idenfy/Documentation/blob/master/resources/sdk/ios/integration/modules_included.png" alt="Embed & Sign " width="700"></kbd>

##### 4. Include internal dependencies
iDenfySDK uses several internal dependencies. Your project should also include those dependencies using CocoaPods or in any another preferred way. 

A list of full dependencies can be found in 
[IdenfySDK.Podspec](https://github.com/idenfy/Documentation/blob/master/resources/sdk/ios/integration/IdenfySDK.podspec).


### 4. Configuring SDK

It is required to provide following configuration:

#### initializeIdenfySDKV2WithManual
##### Swift
```swift
let idenfySettingsV2 = IdenfyBuilderV2()
    .withAuthToken("AUTH_TOKEN")
    .build()

let idenfyController = IdenfyController.shared
idenfyController.initializeIdenfySDKV2WithManual(idenfySettingsV2: idenfySettingsV2)
```

##### Objective-C
```Objective-C
IdenfyBuilderV2 *idenfyBuilderV2 = [[IdenfyBuilderV2 alloc] init];
idenfyBuilderV2 = [idenfyBuilderV2 withAuthToken:authToken];

IdenfySettingsV2 *idenfySettingsV2 = [idenfyBuilderV2 build];

IdenfyController *idenfyController = [IdenfyController shared];
[idenfyController initializeIdenfySDKV2WithManualWithIdenfySettingsV2:idenfySettingsV2];
```

#### V1
##### Swift
```swift
let idenfySettings = IdenfyBuilder()
    .withAuthToken("AUTH_TOKEN")
    .build()

let idenfyController = IdenfyController(idenfySettings: idenfySettings)
```


***Note**: We recommend implementing the initialization of the SDK with the initializeIdenfySDKV2WithManual(). It uses the newest UI/UX and offers more customization options.

### 5. Presenting ViewController

Instance of IdenfyController is required for managing iDenfy ViewController.
Following code will present initial ViewController:
#### V1, initializeIdenfySDKV2WithManual
##### Swift
```swift
let idenfyVC = idenfyController.instantiateNavigationController()         
self.present(idenfyVC, animated: true, completion: nil)
```

##### Objective-C
```Objective-C
UINavigationController *idenfyVC = [idenfyController instantiateNavigationController];
[self presentViewController:idenfyVC animated:YES completion:nil];
```

## Callbacks


#### initializeIdenfySDKV2WithManual
The SDK provides following callback: idenfyIdentificationResult
### Swift
```swift
    idenfyController.handleIdenfyCallbacksWithManualResults(idenfyIdentificationResult: {
            idenfyIdentificationResult
            in
            switch(idenfyIdentificationResult.autoIdentificationStatus){
                
            case .APPROVED:
                break;
            case .FAILED:
                break;
            case .UNVERIFIED:
                break;
            }
            
            switch(idenfyIdentificationResult.manualIdentificationStatus){
            case .APPROVED:
                break;
            case .FAILED:
                break;
            case .WAITING:
                break;
            case .INACTIVE:
                break;
            }
            
        })
```
##### Objective-C
```Objective-C
[idenfyController handleIdenfyCallbacksWithManualResultsWithIdenfyIdentificationResult:^(IdenfyIdentificationResult * _Nonnull idenfyIdentificationResult) {
        NSLog(@"%ld", (long)idenfyIdentificationResult.autoIdentificationStatus);
        switch (idenfyIdentificationResult.autoIdentificationStatus) {
            case AutoIdentificationStatusAPPROVED:
                break;
            case AutoIdentificationStatusFAILED:
                break;
            case AutoIdentificationStatusUNVERIFIED:
                break;
            default:
                break;
        }
        NSLog(@"%ld", (long)idenfyIdentificationResult.manualIdentificationStatus);
        switch (idenfyIdentificationResult.manualIdentificationStatus) {
            case ManualIdentificationStatusAPPROVED:
                break;
            case ManualIdentificationStatusFAILED:
                break;
            case ManualIdentificationStatusWAITING:
                break;
            case ManualIdentificationStatusINACTIVE:
                break;
            default:
                break;
        }
    }];
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

#### V1
The SDK provides following callbacks: onSuccess, onError and onUserExit.
### Swift
```swift
    idenfyController.handleIDenfyCallbacks(
            onSuccess: { (AuthenticationResultResponse) in
             //user proceeded identification. Here you would typically check for Identification status to determine your application flow.
             switch AuthenticationResultResponse.idenfyIdentificationStatus{
                        
                    case .APPROVED: break
                         //user was suspected, while performing
                        
                    case .DENIED: break
                        //identification was denied.
                        
                    case .SUSPECTED: break
                         //identification was approved.
                        
                    case .REVIEWING: break
                        //identification is still under review.
                        
                    }

            }, 

            onError: { (IdenfyErrorResponse) in
            //Error occurred within identification process.
            }, 

            onUserExit: { 
            //User exited the SDK without completing identification process.
            })
```


[Additional information about error responses](https://github.com/idenfy/Documentation/blob/master/pages/StandardErrorMessages.md)

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

All keys are located in [here](https://github.com/idenfy/Documentation/blob/master/resources/sdk/ios/localization/).  You can supply partial translations, meaning if you don't include a translation to particular key, then our SDK will use default keys. In order to see changes add Idenfy.strings to your app target and changes will take effect.

### 2. Forcing specific language
The default language of SDK is selected by the language configurations of the **device**. In order to force particular locale use:
##### Swift
```swift
    IdenfySettingsV2.IdenfyBuilderV2()
    .withSelectedLocale(IdenfyLocaleEnum.EN)
    ...
```

### 3. User flow customization
#### * Language selection skipping
The SDK provides an option to skip **document's issuing country** selection. If the document's issuing country is set in the [identification token generation process](https://github.com/idenfy/Documentation/blob/master/pages/GeneratingIdentificationToken.md) it might be more UX friendlier to skip issuing country selection and navigate the user to document selection screen. 
##### Swift
```swift
    let idenfySettingsV2 = IdenfyBuilderV2()
        .withAuthToken(authToken)
        .withDocumentIssuingCountrySkipped()
        ...
        .build()
    ...
```
*NOTE, make sure that the issuing country is indeed set, when generating an identification token. If issuing country is not set, SDK will behave in a default way - it will navigate user into document issuing country selection screen.

### 4. SSL pinning enabling
By default, the SDK does not utilize SSL pinning as suggested by the **AWS services**.
If you however need this option, you can enable SSL pinning.
Our SSL pinning implementation does follow the [AWS recommendations](https://aws.amazon.com/premiumsupport/knowledge-center/pin-application-acm-certificate/) and we utilize pinning for the Root certificates. They are valid for more than 5+ years. 

However, during this timeframe, major changes can occur and we might be forced to change SSL pinning. Such changes will be notified at least 1 month prior. 

This is why we strongly encourage you to enable this feature only if you are planning to **actively update the SDK**.

##### Swift
```swift
    let idenfySettingsV2 = IdenfyBuilderV2()
        .withAuthToken(authToken)
        .withSSLPinning(true)
        ...
        .build()
    ...
```


## Customizing SDK V1 (optional)

 SDK provides various options for changing identification flow. All requirements can be specified inside of IdenfyBuilder().


 ### 1. Removing initial ViewController

If default document country was selected during **token generation** the terms of services and country information View can be removed.
```swift
    IdenfyBuilder()
    .withPresentInitialView(false)
    ...
```
 ### 2. Custom locale

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
```swift
    IdenfyBuilder()
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

*Note: callbacks will continue to occur as usual in idenfyController.handleIDenfyCallbacks().

 ### 1. Customizing identification results views

Instantiate IdenfyIdentificationResultsSettings and apply settings:

```swift
let idenfyIdentificationResults = IdenfyIdentificationResultsSettings()

    idenfyIdentificationResults.isSuccessResultsViewVisible = true
    idenfyIdentificationResults.isErrorResultsViewVisible = false
    idenfyIdentificationResults.isRetryErrorResultsViewVisible = true
    idenfyIdentificationResults.isRetryingIdentificationAvailable = false
```

|Method name              |Description                     |
|-------------------|-------------------------------|
|`isSuccessResultsViewVisible`   |Sets success results view visible, before providing callback. Default is true.                        |
|`isErrorResultsViewVisible`|Sets general error results view visible, before providing callback. Default is true.                   |
|`isRetryErrorResultsViewVisible`  |Sets retrying identification results view visible. Default is true.                 |
|`isRetryingIdentificationAvailable`  |Enables identification retrying after unsuccessful identification. Default is true.                 |



### 2. Manually dismiss IdentificationResultsViewController

SDK provides optional configuration, which enables to dismiss IdentificationResultsViewController manually. Apply the following settings:
```swift
    idenfyIdentificationResults.isAutoDismissOnSuccessEvent = false
    idenfyIdentificationResults.isAutoDismissOnErrorEvent = false
    idenfyIdentificationResults.isAutoDismissOnUserExitEvent = false
```

|Method name              |Description                     |
|-------------------|-------------------------------|
|`isAutoDismissOnSuccessEvent`   |Handles auto dismissing after receiving identification results. Default is true.                       |
|`isAutoDismissOnErrorEvent`|Handles auto dismissing after error occurrence within identification process. Default is true.               |
|`isAutoDismissOnUserExitEvent`  |Handles auto dismissing after user exits identification, without completing process. Default is true.          |            |

After applying these settings you could dismiss idenfyVC in a following way:

```swift
    idenfyController.handleIDenfyCallbacks(
            onSuccess: { (AuthenticationResultResponse) in
            }, 
                idenfyVC.dismiss(animated: true, completion: nil)

            onError: { (IdenfyErrorResponse) in
                idenfyVC.dismiss(animated: true, completion: nil)

            }, 
            
            onUserExit: { 
                idenfyVC.dismiss(animated: true, completion: nil)

            })
```

 ### 3. Update IdenfyBuilder

Update idenfyBuilder to apply changes:
```swift
    IdenfyBuilder()
    .withCustomIdentificationResultsSettings(idenfyIdentificationResults)
    ...
```

## UI customization

Please take a look at UI customization page:
[UI customization guidelines](https://github.com/idenfy/Documentation/blob/master/pages/IOSUICustomization.md)

## Samples
### Sample SDK code
A following code demonstrates possible iDenfySDK configuration with applied settings:

#### initializeIdenfySDKV2WithManual
##### Swift
```swift
    private func initializeIDenfySDK(authToken:String)
    {
        let idenfyUISettingsV2 = IdenfyUIBuilderV2()
            .withLanguageSelection(true)
            .build()
        
        let idenfySettingsV2 = IdenfyBuilderV2()
            .withAuthToken(authToken)
            .build()
        
        let idenfyController = IdenfyController.shared
        idenfyController.initializeIdenfySDKV2WithManual(idenfySettingsV2: idenfySettingsV2)
        
        self.present(idenfyVC, animated: true, completion: nil)
        idenfyController.handleIdenfyCallbacksWithManualResults(idenfyIdentificationResult: {
            idenfyIdentificationResult
            in
            switch(idenfyIdentificationResult.autoIdentificationStatus){
                
            case .APPROVED:
                break;
            case .FAILED:
                break;
            case .UNVERIFIED:
                break;
            }
            
            switch(idenfyIdentificationResult.manualIdentificationStatus){
            case .APPROVED:
                break;
            case .FAILED:
                break;
            case .WAITING:
                break;
            case .INACTIVE:
                break;
            }
            
        })
    }
```

#### V1
##### Swift
```swift
    private func initializeIDenfySDK(authToken:String)
    {
        let idenfyIdentificationResults = IdenfyIdentificationResultsSettings()
        idenfyIdentificationResults.isAutoDismissOnSuccessEvent = true
        idenfyIdentificationResults.isAutoDismissOnErrorEvent = true
        idenfyIdentificationResults.isAutoDismissOnUserExitEvent = false
        
        let overlayTextSettings = OverlayTextBuilder()
            .withCustomSettings(fontSize: 16, fontColor: UIColor.blue, font:UIFont.systemFont(ofSize: 26))
            .build()

        let cgRect = CGRect(x: 10, y: 10, width:100, height:100)
        let customLoadingView = UIView(frame: cgRect)
        customLoadingView.backgroundColor = UIColor.blue
        
        let idenfyUISettings = IdenfyUIBuilder()
            .withCustomDocumentsOverlayText(overlayDocumentsText: overlayTextSettings)
            .withCustomColors(colorPrimary: UIColor.black, colorPrimaryDark: UIColor.white, colorAccent: UIColor.black)
            .withCustomDocumentBorderColor(borderColor: UIColor.black)
            .withCustomLoadingView(loadingView: customLoadingView)
            .build()
        
        let idenfySettings = IdenfyBuilder()
            .withAuthToken(authToken)
            .withUISettings(idenfyUISettings)
            .withCustomSelectedLocale("en")
            .withCustomIdentificationResultsSettings(idenfyIdentificationResults)
            .withCustomLocalization()
            .build()
        
        let idenfyController = IdenfyController(idenfySettings: idenfySettings)
        
        let idenfyVC = idenfyController.instantiateNavigationController()
        
        self.present(idenfyVC, animated: true, completion: nil)
        idenfyController.handleIDenfyCallbacks(
            onSuccess: { (AuthenticationResultResponse
                ) in
                print(AuthenticationResultResponse)
        },
            onError: { (IdenfyErrorResponse) in
                print(IdenfyErrorResponse.message)
                
        },  onUserExit: {
                print("user exits")
        })
    }
```
### SDK Integration tutorials
For more information visit [SDK integration tutorials](https://github.com/idenfy/Documentation/blob/master/pages/tutorials/mobile-sdk-tutorials.md).


## Advanced Liveness detection
SDK provides advanced liveness recognition. Liveness recognition is attached as separate, optional module inside of the SDK. 

The new major liveness version is released every 6-12 months. Your app must update the liveness module after every major release. If SDK is not updated, it can lead to the **runtime crashes**.

### 1. Update Podfile
In the Podfile **replace** 'iDenfySDK' with following Pod:
```ruby
pod 'iDenfySDK/iDenfyLiveness', '5.4.0'
```

### 2. Update Pods
Run `pod install` to install iDenfySDK or `pod update` to update current iDenfySDK.

### 3. Add Zoom.strings
In order to use localized version of liveness feature add FaceTec.strings to your app module.
In order to use localized version of liveness feature add FaceTec.strings to your app module.

Strings are located in  **../Pods/iDenfySDK/iDenfySDK/IdenfyAssets/IdenfyStrings**

*Note: Contact support for enabling liveness feature.
