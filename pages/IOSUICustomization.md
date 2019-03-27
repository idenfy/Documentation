## Table of contents

*   [Getting started](#getting-started)
*   [Customization with Storyboard](#customization-with-storyboard)
*   [Customization of elements](#customization-of-elements)
*   [Liveness Customization](#liveness-customization)

## Getting started
IOS SDK provides various customization options with *programming code* or *Idenfy.storyboard*.


## Customization with Storyboard
iDenfy SDK groups various components and enables different customization options.

Full design changes can be adjusted with Storyboard.

### 1. Including Storyboard and assets

In order to use custom design you would need to include attached **Idenfy.storyboard** file inside of your target application. 

**IdenfyImages.xcassets** are also required in the target application to match storyboard content.

*Note. Contact support for providing iDenfy resources.

### 2. Updating IdenfySettings

SDK needs to be comnfigured in order to use custom storyboard.

```swift
   IdenfyBuilder()
   ...
    .withCustomStoryboard(true)
```

## Customization of elements
Some elements in SDK could be configured with code to enable easier integration and UI logic reuse.

 ### *  Documents text overlay customization
 #### 1. Creating OverlayText

```swift
 let textBuilder = OverlayTextBuilder()
    .withCustomSettings(fontSize: 16, fontColor: UIColor.blue, font:UIFont.systemFont(ofSize: 26))
    .build()
```
 #### 2. Updating IdenfyUISettings

 ```swift
   IdenfyUIBuilder()
    ...
    withCustomDocumentsOverlayText(overlayDocumentsText: textBuilder)
```

## Liveness Customization

iDenfy SDK provides additional liveness customization.

 ### 1. Creating IdenfyLivenessUIHelper

 ```swift
 let idenfyLivenessUISettings = IdenfyLivenessUISettings()
```
 ### 2. Applying settings

 Atrributes of IdenfyLiveness UISettings

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
    ...
    .withLivenessUISettings(livenessUISettings: idenfyZoomSettings)
    .build()
```





