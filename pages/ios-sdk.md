## Table of contents
*   [Changelog](#changelog)
*   [Getting started](#getting-started)
*   [Callbacks](#callbacks)
*   [Customizing SDK V2 (optional)](#customizing-sdk-v2-optional)
*   [Customizing SDK V1 (optional)](#customizing-sdk-v1-optional)
*   [Customizing results callbacks V2 (optional)](#customizing-results-callbacks-v2-optional)
*   [Customizing results callbacks V1 (optional)](#customizing-results-callbacks-v1-optional)
*   [UI customization](#ui-customization)
*   [Sample SDK code](#sample-sdk-code)
*   [Advanced Liveness detection](#advanced-liveness-detection)


## Changelog
All updates will be written in this section.

Our SDK versioning conforms to [Semantic Versioning 2.0.0](https://semver.org/).

The structure of our changes follow practices from [keep a changelog](https://keepachangelog.com/en/1.0.0/).


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

Run `pod install` to get the SDK or `pod update` to update current iDenfySDK.

### 4. Configuring SDK

It is required to provide following configuration:
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

### 5. Presenting ViewController

Instance of IdenfyController is required for managing iDenfy ViewController.
Following code will present initial ViewController:
#### V2, V1
##### Swift
```swift
let idenfyVC = idenfyController.instantiateNavigationController()         
self.present(idenfyVC, animated: true, completion: nil)
```

## Callbacks

SDK provides following callbacks: onSuccess, onError and onUserExit.

Following method will provide callbacks from the SDK:

#### V1, V2
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

All keys are located in [here](https://github.com/idenfy/Documentation/blob/master/resources/sdk/ios/localization/).  You can supply partial translations, meaning if you don't include a translation to particular key, then our SDK will use default keys. In order to see changes add Idenfy.strings to your app target and changes will take effect.

### 2. Forcing specific language
The default language of SDK is selected by the language configurations of the **device**. In order to force particular locale use:
##### Java
```java
    IdenfySettingsV2.IdenfyBuilderV2()
    .withSelectedLocale(IdenfyLocaleEnum.EN)
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

## Sample SDK code
A following code demonstrates possible iDenfySDK configuration with applied settings:
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


 ## Advanced Liveness detection
SDK provides advanced liveness recognition. Liveness recognition is attached as separate, optional module inside of the SDK. 

New major liveness version is released every 6-12 months. After major version release SDK must be updated also.

In the Podfile **replace** 'iDenfySDK' with following Pod:
```ruby
pod 'iDenfySDK/iDenfyLiveness'
```
Run `pod install` to install iDenfySDK or `pod update` to update current iDenfySDK.
 
*Note: Contact support for enabling liveness feature.
