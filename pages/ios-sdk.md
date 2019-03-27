## Table of contents

*   [Getting started](#getting-started)
*   [Callbacks](#callbacks)
*   [Customising flow](#customising-flow)
*   [UI Customisation](#ui-customisation)
*   [Advanced Liveness detection](#advanced-liveness-detection)

## Getting started

* SDK supports iOS 9.0
* SDK supports all versions previous to Swift 5.0 starting from version 1.0* until 1.2*
* SDK supports Swift 5.0 and Xcode 10.2 starting from version 1.2*

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

*Swift 4.2 or below should use:
```ruby
pod 'iDenfySDK', '<1.2'
```

Run `pod install` to get the sdk.

### 4. Configuring SDK

It is required to provide following configuration:
### Swift
```swift
 let idenfySettings = IdenfyBuilder()
    .withAuthToken("AUTH_TOKEN")
    .build()

    let idenfyController = IdenfyController(idenfySettings: idenfySettings)
```
### 5. Presenting ViewController

idenfyController instance is responsible for creating ViewController.
### Swift
```swift
   let idenfyVC = idenfyController.instantiateNavigationController()         

   self.present(idenfyVC, animated: true, completion: nil)
```
This code will present initial ViewController

## Callbacks
SDK provides following callbacks: onSuccess, onError and onUserExit.

Following method will provide callbacks from the SDK:

After receiving **onSuccess or onError** response it is suggested to check status via API call.

### Swift
```swift
    idenfyController.handleIDenfyCallbacks(
            onSuccess: { (AuthenticationResultResponse) in
            //user procceeded identification. Here you would typically check for Identification status and check response using API call
            }, 

            onError: { (IdenfyErrorResponse) in
            //Error response
            }, 
            onUserExit: { 
            //User exited the SDK
            })
```

Alternatively each callback can be listened separately, by only calling particular closure.

 [Additional information about callbacks](https://github.com/idenfy/Documentation/blob/master/pages/StandardErrorMessages.md)

 ## Customising flow
 SDK provides various options for changing identification flow. All requirements can be specified inside of IdenfyBuilder()


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
 - Polish (es) PL
 - Russian (es) RU
 - Lithuanian (es) LT

The language of SDK is selected by the language configurations of the **device**. In order to setup custom localization the following method must be called
```swift
   IdenfyBuilder()
    .withCustomSelectedLocale("locale")
    ...
```
## UI Customisation

SDK provides various ways of changing UI for better design integration.
 ### 1. UI settings

### Swift
```swift
let idenfyUISettings = IdenfyUIBuilder()
    .withCustomColors(colorPrimary: UIColor, colorPrimaryDark: UIColor, colorAccent: UIColor)
    .withCustomLoadingView(loadingView: UIView?)
    .build()
```
Provide created UISettings when initializing idenfySettings:
```swift
    let idenfySettings = IdenfyBuilder()
    .withUISettings(idenfyUISettings)
    ...
    
```
Default colors have following values and represent UI elements in the ViewControllers:
```swift
var idenfyColorPrimary:UIColor = UIColor(red: 54.0/255.0, green: 70.0/255.0, blue: 93.0/255.0, alpha: 1.0)
var idenfyColorPrimaryDark:UIColor = UIColor(red: 43/255.0, green: 56/255.0, blue: 74/255.0, alpha: 1.0)
var idenfyColorAccent:UIColor = UIColor(red:139/255.0, green: 199/255.0, blue: 224/255.0, alpha: 1.0)    
```
 ### 2. Custom Storyboard
 
Additionaly SDK provides storyboard file, which contains whole design of an SDK. 

The storyboard file can be *fully customised*. The only requirement is to include storyboard file in the **app folder** of your application and provide following method:

```swift
   IdenfyBuilder()
    .withCustomStoryboard(true)
    ...
```
*Note: If custom storyboard is selected, UISettings will still override Interface Builder.

 ## Advanced Liveness detection
SDK provides advanced liveness recognition. Liveness recognition is attached as separate, optional module inside of the SDK. 
 
Attached liveness SDK will sync with **core** Idenfy SDK.

In the Podfile add following Pod:
```ruby
pod 'iDenfySDK/iDenfyLiveness'
```
Run `pod install` to add additional Pod
 
*Note: Contact support for enabling liveness feature
