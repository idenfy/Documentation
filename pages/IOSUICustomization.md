## Table of contents

*   [Getting started](#getting-started)
*   [Customization V1](#customization-v1)
*   [Customization V2](#customization-v2)
*   [Liveness customization](#liveness-customization)

## Getting started
IOS SDK provides various customization options with *programming code* or *Idenfy.storyboard*.

### 1. Create IdenfyUISettings

Create an instance of IdenfyUISettings class:

### Swift
```swift
let idenfyUISettings = IdenfyUIBuilder()
    .build()
```
### 2.Update IdenfyUISettings

```swift
let idenfySettings = IdenfyBuilder()
    .withUISettings(idenfyUISettings)
    ...
    .build()
    
```
## Customization V1

Customization options for V1 are final. For better options switch to V2.

### Customization with storyboard
iDenfy SDK groups various components and enables different customization options.

Full design changes can be adjusted with Idenfy storyboard.

#### 1. Including Storyboard and assets

In order to use custom design you would need to include attached **Idenfy.storyboard** file inside of your target application. 

**IdenfyImages.xcassets** are also required in the target application to match storyboard content.

*Note: Contact support for providing iDenfy resources.

#### 2. Updating IdenfySettings

SDK needs to be configured in order to use custom storyboard.

```swift
    IdenfyBuilder()
    .withCustomLocalStoryboard(true)
    ...
```
*Note: If custom storyboard is selected, UISettings **will override** Interface Builder.

### Customization of colors

SDK provides colors customization:
```swift
let idenfyUISettings = IdenfyUIBuilder()
    .withCustomColors(colorPrimary: UIColor, colorPrimaryDark: UIColor, colorAccent: UIColor)
    .withCustomDocumentBorderColor(borderColor: UIColor.black)
    ...
```

Information about colors:

|Color name              |Description                     |Default color value
|-------------------|-------------------------------|------------------------------------
|`idenfyColorPrimary`   |Defines the default theme color.                 |UIColor(red: 54.0/255.0, green: 70.0/255.0, blue: 93.0/255.0, alpha: 1.0)
|`idenfycolorPrimaryDark`|Defines the default color of the retake button. |UIColor(red: 43/255.0, green: 56/255.0, blue: 74/255.0, alpha: 1.0)
|`idenfycolorAccent`  |Defines the color of results spinner and proceed button color.             |UIColor(red:139/255.0, green: 199/255.0, blue: 224/255.0, alpha: 1.0)
|`idenfyDocumentBorderColor`  |Defines the color of the document border, which appears during identification flow. |UIColor(red:139/255.0, green: 199/255.0, blue: 224/255.0, alpha: 1.0)  

### Customization of components
Some elements in SDK could be configured with code to enable easier integration and UI logic reuse.

 #### *  Documents text overlay customization
 ##### 1. Creating OverlayText

```swift
 let overlayText = OverlayTextBuilder()
    .withCustomSettings(fontSize: 16, fontColor: UIColor.blue, font:UIFont.systemFont(ofSize: 26))
    ...
```
 ##### 2. Updating IdenfyUISettings

 ```swift
    IdenfyUIBuilder()
    .withCustomDocumentsOverlayText(overlayDocumentsText: overlayText)
    ...
```

## Customization V2
### Customization by changing views from idenfyviews module:
All UI elements are located in the separate module - idenfyviews. Classes are marked as public, so you can override them.
#### 1. Including idenfyviews
```swift
import idenfyviews
```

#### 2. Applying customization
Take for example IdenfyConfirmationViewUISettingsV2 settings.

```swift
@objc open class IdenfyConfirmationViewUISettingsV2:NSObject {
    
    // Idenfy Confirmation View Colors

    public static var idenfyDocumentConfirmationViewBackgroundColor = IdenfyCommonColors.idenfyBackgroundColorV2
    public static var idenfyDocumentConfirmationViewTitleTextColor = IdenfyCommonColors.idenfySecondColorV2
    public static var idenfyDocumentConfirmationViewDescriptionTextColor = IdenfyCommonColors.idenfySecondColorV2
    public static var idenfyDocumentConfirmationViewDescriptionHighlightedTextColor = IdenfyCommonColors.idenfyMainColorV2
    public static var idenfyDocumentConfirmationViewBeginIdentificationButtonTextColor = IdenfyCommonColors.idenfyWhite
    public static var idenfyDocumentConfirmationViewDocumentStepTitleTextColor = IdenfyCommonColors.idenfySecondColorV2
    public static var idenfyDocumentConfirmationViewDocumentStepTitleHighlightedTextColor = IdenfyCommonColors.idenfyMainColorV2
    public static var idenfyDocumentConfirmationViewUploadDocumentPhotoTitleTextColor = IdenfyCommonColors.idenfySecondColorV2
    public static var idenfyDocumentConfirmationViewDocumentStepCellNumberTextColor = IdenfyCommonColors.idenfyWhite
    public static var idenfyDocumentConfirmationViewDocumentStepCellTitleTextColor = IdenfyCommonColors.idenfySecondColorV2
    public static var idenfyDocumentConfirmationViewContentMaskForegroundColor = IdenfyCommonColors.idenfyBackgroundColorV2.withAlphaComponent(0.9)
    public static var idenfyDocumentConfirmationViewUploadIconTintColor:UIColor? = IdenfyCommonColors.idenfyMainColorV2
    public static var idenfyDocumentConfirmationViewDocumentStepCircleTintColor:UIColor? = IdenfyCommonColors.idenfyMainColorV2

    // Idenfy Confirmation View Fonts

    public static var idenfyDocumentConfirmationViewTitleFont = UIFont(name: ConstsIdenfyFonts.idenfyFontBoldV2, size: 22)
    public static var idenfyDocumentConfirmationViewDescriptionFont = UIFont(name: ConstsIdenfyFonts.idenfyFontRegularV2, size: 13)
    public static var idenfyDocumentConfirmationViewDescriptionHighlightedFont = UIFont(name: ConstsIdenfyFonts.idenfyFontBoldV2, size: 13)
    public static var idenfyDocumentConfirmationViewDocumentStepTitleFont = UIFont(name: ConstsIdenfyFonts.idenfyFontBoldV2, size: 13)
    public static var idenfyDocumentConfirmationViewUploadTitleFont = UIFont(name: ConstsIdenfyFonts.idenfyFontRegularV2, size: 13)
    public static var idenfyDocumentConfirmationViewDocumentStepNumberFont = UIFont(name: ConstsIdenfyFonts.idenfyFontBoldV2, size: 11)
    public static var idenfyDocumentConfirmationViewDocumentStepFont = UIFont(name: ConstsIdenfyFonts.idenfyFontRegularV2, size: 13)

    // Idenfy Confirmation View Style

    public static var idenfyDocumentConfirmationViewDocumentStepCellHeight = CGFloat(30)
    
}
```
You can customize it in following manner:

Example:
```swift
    IdenfyConfirmationViewUISettingsV2.idenfyDocumentConfirmationViewBackgroundColor = UIColor.red
    IdenfyConfirmationViewUISettingsV2.idenfyDocumentConfirmationViewTitleTextColor = UIColor.red
```

#### 3. Applying SDK wide color changes
If **color and assets changes** are the only requirement, then it can be easily customized by changing main colors.

Information about colors:

|Color name              |Description                     |Default color value
|-------------------|-------------------------------|------------------------------------
|`idenfyMainColorV2`   |Defines the color of most single colored assets and focused parts in SDK.                 |#536DFE
|`idenfyMainDarkerColorV2`|Defines the color of some focused parts in SDK, similar to idenfyMainColorV2.  |#5D7CE4
|`idenfyBackgroundColorV2`   |Defines the background color.            |#FBFBFB
|`idenfySecondColorV2`|Defines the text color.    |#F2353B4E
|`idenfyGradientAccentV2`   |Defines the second color of gradient. Currently used in confirmation buttons.               |#8D6CFB

You can customize it in a following manner:

Example:
```swift
    IdenfyCommonColors.idenfyMainColorV2 = UIColor.green
    IdenfyCommonColors.idenfyMainDarkerColorV2 = UIColor.green
```

Colors also are applied on images, which use a single color from *IdenfyImagesV2.xcassets* .If perhaps you decided to override our provided images with more sophisticated icons, which use more than 1 color, then you can easily disable tint on images. You need set color values as *nil*.

Example:
```swift
    IdenfyConfirmationViewUISettingsV2.idenfyDocumentConfirmationViewDocumentStepCircleTintColor = nil
    IdenfyConfirmationViewUISettingsV2.idenfyDocumentConfirmationViewUploadIconTintColor = nil
    IdenfyToolbarUISettingsV2.idenfyDefaultToolbarLogoIconTintColor = nil
    IdenfyToolbarUISettingsV2.idenfyDefaultToolbarBackIconTintColor = nil
    IdenfyToolbarUISettingsV2.idenfyLanguageSelectionToolbarLanguageSelectionIconTintColor = UIColor.yellow
    IdenfyToolbarUISettingsV2.idenfyLanguageSelectionToolbarCloseIconTintColor = nil
    IdenfyToolbarUISettingsV2.idenfyCameraPreviewSessionToolbarBackIconTintColor = nil
    IdenfyIdentificationResultsViewUISettingsV2.idenfyIdentificationResultsDividerIconStatusErrorTintColor = nil
    IdenfyIdentificationResultsViewUISettingsV2.idenfyIdentificationResultsDividerIconStatusLoadingTintColor = nil
```


### Customization by providing custom IdenfyViewsV2 class:
For more advanced customization (fonts, constraints, layout structure, etc.) it is better to override our layouts. All layouts used in IdenfySDK are located in idenfyviews module.


#### 1. Create an instance of IdenfyViewsV2 
Use IdenfyViewsBuilderV2 to create an instance of IdenfyViewsV2 with your custom views, which conform to protocols provided by the iDenfySDK. Take a look at the methods of the IdenfyViewsBuilderV2 class.
```swift
let idenfyViewsV2:IdenfyViewsV2 = IdenfyViewsBuilderV2()
            .withSplashScreenV2View(SplashScreenV2View())
            ...
            .build()
```
#### 2. Initiliaze iDenfySDK with an instance of IdenfyViewsV2
Pass created instance of the IdenfyViewsV2 class to the initializeIdenfySDKV2WithManual() method.
```swift
 idenfyController.initializeIdenfySDKV2WithManual(idenfySettingsV2: idenfySettingsV2, idenfyViewsV2: idenfyViewsV2)
```
### Customization with IdenfyUISettingsV2:

#### * Adding instructions in camera session.
iDenfySDK provides informative instructions during identification session. They can provide valuable information for the user and help to tackle common issues: bad lightning, wrong document side and etc. Instructions can be customized, by changing all UI elements or even using your own MP4 video files.
Instructions are configured by your backend settings and can be overriden with the SDK settings.

#### 1. Enable instructions in IdenfyUISettingsV2
 ```swift
  let idenfyUISettingsV2 = IdenfyUIBuilderV2()
            .withInstructions(true)
            .build()
```




## Liveness Customization

iDenfy SDK provides additional liveness customization.

### 1. Creating IdenfyLivenessUIHelper
#### V1, V2

 ```swift
let idenfyLivenessUISettings = IdenfyLivenessUISettings()
```

### 2.1 Applying regular settings
If you only need color, text, or width customization, you can use properties from the IdenfyLivenessUISettings class.
#### V1, V2
#### IdenfyLivenessUISettings

 ```swift
    @objc public class IdenfyLivenessUISettings: NSObject {
    // Used for different ui parts
    public var idenfyLivenessPrimaryColor = UIColor.white
    public var idenfyLivenessAccentColor = UIColor(red: 139 / 255.0, green: 199 / 255.0, blue: 224 / 255.0, alpha: 1.0)
    public var idenfyLivenessTextColor = UIColor.black

    // Liveness session feedback settings
    public var livenessFeedbackBackgroundColor = UIColor(red: 139 / 255.0, green: 199 / 255.0, blue: 224 / 255.0, alpha: 1.0)
    public var livenessFeedbackFont: UIFont = UIFont(name: ConstsIdenfyFonts.idenfyFontBoldV2, size: 18) ?? UIFont.boldSystemFont(ofSize: 18)
    public var livenessFeedbackFontSizeMobile: CGFloat?
    public var livenessFeedbackFontSizeTablet: CGFloat?
    public var livenessFeedbackFontColor: UIColor?

    // Liveness session frame settings
    public var livenessFrameBackgroundColor: UIColor = UIColor.black.withAlphaComponent(0.72)
    public var livenessFrameColor: UIColor?
    public var livenessFrameWidth: Int32? = 0
    
    //Liveness session cancel button settings
    public var livenessCancelButtonImage = UIImage(named: "idenfy_ic_liveliness_camera_session_cancel_image", in: Bundle(identifier: "com.idenfy.idenfysdk"), compatibleWith: nil)

    // Liveness session progress settings
    public var livenessIdentificationOvalProgressColor1 = UIColor(red: 139 / 255.0, green: 199 / 255.0, blue: 224 / 255.0, alpha: 1.0)
    public var livenessIdentificationProgressStrokeColor = UIColor(red: 139 / 255.0, green: 199 / 255.0, blue: 224 / 255.0, alpha: 1.0)
    public var livenessIdentificationOvalProgressColor2 = UIColor(red: 139 / 255.0, green: 199 / 255.0, blue: 224 / 255.0, alpha: 1.0)
    public var livenessIdentificationProgressStrokeWidth: Int32 = 4
    public var livenessIdentificationStrokeWidth: Int32 = 3
    public var livenessIdentificationProgressRadialOffset: Int32 = 6
    // Liveness session overlay settings
    public var livenessOverlayBrandingImage = UIImage(named: "idenfy_ic_liveliness_overlay_branding_image", in: Bundle(identifier: "com.idenfy.idenfysdk"), compatibleWith: nil)

    // Liveness ready screen settings
    public var livenessReadyScreenForegroundColor: UIColor?
    public var livenessReadyScreenBackgroundColors: [UIColor]?
    public var livenessReadyScreenTextBackgroundColor: UIColor?
    public var livenessReadyScreenButtonBorderColor: UIColor?
    public var livenessReadyScreenButtonBorderWidth: Int32? = 1
    public var livenessReadyScreenButtonCornerRadius: Int32? = 4
    public var livenessReadyScreenButtonBackgroundNormalColor: UIColor?
    public var livenessReadyScreenButtonBackgroundHighlightedColor: UIColor?
    public var livenessReadyScreenShowBrandingImage: Bool? = true
    
    //Camera permissions screen
    
    public var livenessCameraPermissionsScreenImage = UIImage(named: "idenfy_ic_liveliness_camera_permissions_screen_image", in: Bundle(identifier: "com.idenfy.idenfysdk"), compatibleWith: nil)

    // Liveness result screen settings
    public var livenessResultScreenForegroundColor: UIColor?
    public var livenessResultScreenIndicatorColor: UIColor?
    public var livenessResultScreenUploadProgressFillColor: UIColor?
    public var livenessResultScreenUploadProgressTrackColor: UIColor?
    public var livenessResultScreenShowUploadProgressBar: Bool? = true
    public var livenessResultScreenResultAnimationSuccessBackgroundImage = UIImage(named: "idenfy_ic_liveliness_results_success_icon_background", in: Bundle(identifier: "com.idenfy.idenfysdk"), compatibleWith: nil)


    public var livenessCustomUISettings: ZoomCustomization?

    // ID check customization
    public var livenessIdCheckCustomization = LivenessIdCheckCustomization()

    }
```

#### LivenessIdCheckCustomization
```swift
@objc public class LivenessIdCheckCustomization: NSObject {
    public var buttonBackgroundNormalColor: UIColor?
    public var buttonBackgroundHighlightColor: UIColor?
    public var captureScreenTextBackgroundColor: UIColor?
    public var reviewScreenTextBackgroundColor: UIColor?
    public var captureFrameStrokeColor: UIColor?
}
```

### 2.2 Applying full customization
If you require more changes, you can directly set **livenessCustomUISettings** property in the *IdenfyLivenessUISettings* with your own ZoomCustomization. 
*Note 
It will override all other set properties of the IdenfyLivenessUISettings class.

### 3. Updating IdenfyUISettings

#### V1
```swift
     let idenfyUISettings = IdenfyUIBuilder()
            .withLivenessUISettings(idenfyLivenessUISettings)
            ...
            .build()
```

#### V2
```swift
     let idenfyUISettingsV2 = IdenfyUIBuilderV2()
            .withLivenessUISettings(idenfyLivenessUISettings)
            ...
            .build()
```





