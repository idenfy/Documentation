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

* SDK supports iOS 9.0.
* SDK supports all versions previous to Swift 5.0 starting from version 1.0* until 1.2*.
* SDK supports Swift 5.0 and Xcode 10.2 starting from version 1.2*.

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
pod 'iDenfySDK'
```
Support for Swift versions:

*Swift <= 4.2:
```ruby
pod 'iDenfySDK', '<1.2'
```

*Swift 5.0:
```ruby
pod 'iDenfySDK', '<1.3'
```
*Swift >= 5.1 (module stability):
```ruby
pod 'iDenfySDK'
```

#### Manual
##### 1. Download iDenfySDK
[Download](https://s3-eu-west-1.amazonaws.com/sdk.builds/ios-sdk/3.2.1/iDenfySDK.zip) latest iDenfySDK builds.
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

#### WithManualResults
##### Swift
```swift
let idenfySettingsV2 = IdenfyBuilderV2()
    .withAuthToken("AUTH_TOKEN")
    .build()

let idenfyController = IdenfyController.shared
idenfyController.initializeIdenfySDKWithManualResults(idenfySettingsV2: idenfySettingsV2)
```

#### V2
##### Swift
```swift
let idenfySettingsV2 = IdenfyBuilderV2()
    .withAuthToken("AUTH_TOKEN")
    .build()

let idenfyController = IdenfyController.shared
idenfyController.initializeIdenfySDKV2(idenfySettingsV2: idenfySettingsV2)
```

#### V1
##### Swift
```swift
let idenfySettings = IdenfyBuilder()
    .withAuthToken("AUTH_TOKEN")
    .build()

let idenfyController = IdenfyController(idenfySettings: idenfySettings)
```


***Note**: We recommend to implement the initialization with the manual identification results. The regular V2 initialization will be removed in the future, while initialization with the manual identification results provides easier integration, existing **V2 version** customization options and similar callbacks handling to our [iFrame solution](https://github.com/idenfy/Documentation/blob/master/pages/ClientRedirectToWebUiIframe.md). 

### 5. Presenting ViewController

Instance of IdenfyController is required for managing iDenfy ViewController.
Following code will present initial ViewController:
#### V2, V1, WithManualResults
##### Swift
```swift
let idenfyVC = idenfyController.instantiateNavigationController()         
self.present(idenfyVC, animated: true, completion: nil)
```

## Callbacks


#### WithManualResults
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
            case .INACTIVE:
                break;
            }
            
        })
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
|`APPROVED`   |The user completed an identification flow, was verified manually and the identification status, provided by a manual reviewer, is APPROVED.
|`FAILED`|The user completed an identification flow, was verified manually and the identification status, provided by a manual reviewer, is FAILED.
|`INACTIVE`   |The user was only verified by an automated platform, not by a manual reviewer.

#### V1, V2
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
##### Java
```java
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
*NOTE, make sure that issuing country is indeed set, when generating an identification token. If issuing country is not set, SDK will behave in a default way - it will navigate user into document issuing country selection screen.

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

#### WithManualResults
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
        idenfyController.initializeIdenfySDKWithManualResults(idenfySettingsV2: idenfySettingsV2)
        
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
            case .INACTIVE:
                break;
            }
            
        })
    }
```


#### V2
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
        idenfyController.initializeIdenfySDKV2(idenfySettingsV2: idenfySettingsV2)
        
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
pod 'iDenfySDK/iDenfyLiveness'
```
### 2. Update Pods
Run `pod install` to install iDenfySDK or `pod update` to update current iDenfySDK.

### 3. Add Zoom.strings
In order to use localized version of liveness feature add Zoom.strings to your app module.

Strings are located in  **../Pods/iDenfySDK/iDenfySDK/IdenfyAssets/IdenfyStrings**

*Note: Contact support for enabling liveness feature.
