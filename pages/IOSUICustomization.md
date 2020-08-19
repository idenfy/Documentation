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
### Customization by changing views from idenfyviews module.
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


### Customization by overriding idenfyviews module
For more advanced customization (fonts, constraints, layout structure and etc.) it is better to override our layouts. All layouts used in IdenfySDK are located in idenfyviews module. All code is not compiled and can easily be edited. 

#### 1. Download sample
[Download](https://github.com/idenfy/Documentation/blob/master/resources/sdk/ios/integration/idenfysdk-ui-editor.zip) sample, which will help generate an idenfyviews framework. 

#### 2. Customize idenfyviews
Now you can edit any files in idenfyviews. Things to keep in mind:
- Don't change names of resources
- Strings can be overwritten. For changing strings you should edit Idenfy.strings file


#### 3. Build an universal idenfyviews framework
After finishing customizing views you should generate an universal framework. Simply select **idenfyviewsUniversal** target and run the framework in Xcode. Output will be generated in Output folder.
*Note: You should run framework on both Simulator and actual device in order to generate all architectures.

<kbd><img src="https://github.com/idenfy/Documentation/blob/master/resources/sdk/ios/integration/idenfyviews_compiled.png" alt="Compiled idenfyviews" width="700"></kbd>

#### 4. Replace idenfyviews framework
In order to see changes you should replace default idenfyviews framework with a new, customized version. Simply open **../Pods/iDenfySDK/iDenfySDK/IdenfySDK** and replace current idenfyviews with a new version.

*Note: Every time you run pod update or pod install your customized idenfyviews.framework will be overwritten by default idenfyviews. This is why it is necessary to make sure that your customized version is used instead of default. For automating this process you should add iDenfySDK [manually](https://github.com/idenfy/Documentation/blob/master/pages/ios-sdk.md#3-adding-the-sdk-dependency).

### Adding instructions in camera session.
iDenfySDK provides informative instructions during identification session. They can provide valuable information for the user and help to tackle common issues: bad lightning, wrong document side and etc. Instructions can be customized, by changing all UI elements or even using your own MP4 video files.
#### 1. Enable instructions in IdenfyUISettingsV2
 ```swift
  let idenfyUISettingsV2 = IdenfyUIBuilderV2()
            .withInstructions(true)
            .build()
```




## Liveness Customization

iDenfy SDK provides additional liveness customization.

 ### 1. Creating IdenfyLivenessUIHelper

 ```swift
 let idenfyLivenessUISettings = IdenfyLivenessUISettings()
```
 ### 2. Applying settings

 iDenfySDK provides the following attributes for liveness customization:

 ```swift
    //Used for different ui parts
    public var  idenfyLivenessPrimaryColor = UIColor.white
    public var  idenfyLivenessAccentColor = UIColor(red:139/255.0, green: 199/255.0, blue: 224/255.0, alpha: 1.0)
    public var  idenfyLivenessTextColor = UIColor.black
    
    //Liveness session feedback settings
    public var  livenessFeedbackBackgroundColor = UIColor(red:139/255.0, green: 199/255.0, blue: 224/255.0, alpha: 1.0)
    public var  livenessFeedbackFont : UIFont = UIFont(name: ConstsIdenfyFonts.idenfyFontBoldV2, size: 18) ?? UIFont.boldSystemFont(ofSize: 18)
    public var  livenessFeedbackFontSizeMobile : CGFloat?
    public var  livenessFeedbackFontSizeTablet : CGFloat?
    public var  livenessFeedbackFontColor : UIColor?
    
    //Liveness session frame settings
    public var  livenessFrameBackgroundColor : UIColor = UIColor.black.withAlphaComponent(0.72)
    public var livenessFrameColor: UIColor?
    public var livenessFrameWidth: Int32? = 0
    
    //Liveness session progress settings
    public var  livenessIdentificationOvalProgressColor1 = UIColor(red:139/255.0, green: 199/255.0, blue: 224/255.0, alpha: 1.0)
    public var  livenessIdentificationProgressStrokeColor = UIColor(red:139/255.0, green: 199/255.0, blue: 224/255.0, alpha: 1.0)
    public var  livenessIdentificationOvalProgressColor2 = UIColor(red:139/255.0, green: 199/255.0, blue: 224/255.0, alpha: 1.0)
    public var livenessIdentificationProgressStrokeWidth: Int32 = 4
    public var livenessIdentificationStrokeWidth: Int32 = 3
    public var livenessIdentificationProgressRadialOffset: Int32 = 6
    //Liveness session overlay settings
    public var livenessOverlayBrandingImage = UIImage(named: "idenfy_ic_idenfy_logo_vector_v1", in: Bundle(identifier: "com.idenfy.idenfysdk"), compatibleWith: nil)
    
    //Liveness ready screen settings
    public var livenessReadyScreenForegroundColor: UIColor?
    public var livenessReadyScreenBackgroundColors: [UIColor]?
    public var livenessReadyScreenTextBackgroundColor: UIColor?
    public var livenessReadyScreenButtonBorderColor: UIColor?
    public var livenessReadyScreenButtonBorderWidth: Int32? = 1
    public var livenessReadyScreenButtonCornerRadius: Int32? = 4
    public var livenessReadyScreenButtonBackgroundNormalColor: UIColor?
    public var livenessReadyScreenButtonBackgroundHighlightedColor: UIColor?
    public var livenessReadyScreenShowBrandingImage: Bool? = true
    
    //Liveness result screen settings
    public var livenessResultScreenForegroundColor: UIColor?
    public var livenessResultScreenIndicatorColor: UIColor?
    public var livenessResultScreenUploadProgressFillColor: UIColor?
    public var livenessResultScreenUploadProgressTrackColor: UIColor?
    public var livenessResultScreenShowUploadProgressBar: Bool? = true
    public var livenessResultScreenResultAnimationSuccessBackgroundImage =  UIImage(named: "idenfy_ic_liveliness_results_success_icon_background_v1", in: Bundle(identifier: "com.idenfy.idenfysdk"), compatibleWith: nil)
    
    //Full custom settings
    public var livenessCustomUISettings : ZoomCustomization?
```
 ### 3. Updating IdenfyUISettings

```swift
let idenfyUISettings = IdenfyUIBuilder()
    .withLivenessUISettings(livenessUISettings: idenfyUISettings)
    ...
```





