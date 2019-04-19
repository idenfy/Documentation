## Table of contents

*   [Getting started](#getting-started)
*   [Customization with storyboard](#customization-with-storyboard)
*   [Customization of colors](#customization-of-colors)
*   [Customization of components](#customization-of-components)
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

## Customization with storyboard
iDenfy SDK groups various components and enables different customization options.

Full design changes can be adjusted with Idenfy storyboard.

### 1. Including Storyboard and assets

In order to use custom design you would need to include attached **Idenfy.storyboard** file inside of your target application. 

**IdenfyImages.xcassets** are also required in the target application to match storyboard content.

*Note. Contact support for providing iDenfy resources.

### 2. Updating IdenfySettings

SDK needs to be configured in order to use custom storyboard.

```swift
    IdenfyBuilder()
    .withCustomStoryboard(true)
    ...
```
*Note: If custom storyboard is selected, UISettings **will override** Interface Builder.

## Customization of colors

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

## Customization of components
Some elements in SDK could be configured with code to enable easier integration and UI logic reuse.

 ### *  Documents text overlay customization
 #### 1. Creating OverlayText

```swift
 let textBuilder = OverlayTextBuilder()
    .withCustomSettings(fontSize: 16, fontColor: UIColor.blue, font:UIFont.systemFont(ofSize: 26))
    ...
```
 #### 2. Updating IdenfyUISettings

 ```swift
    IdenfyUIBuilder()
    .withCustomDocumentsOverlayText(overlayDocumentsText: textBuilder)
    ...
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
 
 //Allows you to change color of the feedback bar shown during Liveness
idenfyLivenessUISettings.livenessFeedbackBackgroundColor  = UIColor.blue

//Allows you to change color of the feedback FontColor shown during Liveness
idenfyLivenessUISettings.livenessFeedbackFontColor = UIColor.blue

// Color of the mainscreen, Pre-Enrollment, and Retry screens' background
idenfyLivenessUISettings.livenessMainBackgroundColor = UIColor.blue

// Color of the mainscreen, Pre-Enrollment, and Retry screens' foreground
idenfyLivenessUISettings.livenessMainForegroundColor = UIColor.blue

// Color of the background surrounding the oval outline during Liveness
idenfyLivenessUISettings.livenessFrameBackgroundColor = UIColor.blue

// Color of the animated 'progress spinner' strokes during Liveness
idenfyLivenessUISettings.livenessIdentificationOvalProgressColor1 = UIColor.blue

idenfyLivenessUISettings.livenessIdentificationOvalProgressColor2 = UIColor.white

// Color of the outline of the oval during Liveness
idenfyLivenessUISettings.livenessIdentificationProgressStrokeColor = UIColor.blue

// Thickness of the outline of the oval during Liveness
idenfyLivenessUISettings.livenessIdentificationProgressStrokeWidth = 8.0

// Radial offset of the animated 'progress spinner' strokes relative to the outermost bounds of the oval outline. As this value increases, animations move closer toward the oval's center
idenfyLivenessUISettings.livenessIdentificationProgressRadialOffset = 16.0
```
 ### 3. Updating IdenfyUISettings

```swift
let idenfyUISettings = IdenfyUIBuilder()
    .withLivenessUISettings(livenessUISettings: idenfyZoomSettings)
    ...
```





