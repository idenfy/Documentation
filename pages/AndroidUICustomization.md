## Table of contents

*   [Getting started](#getting-started)
*   [Customization V1](#customization-v1)
*   [Customization V2](#customization-v2)
*   [Liveness customization](#liveness-customization)

## Getting started
Android SDK provides various customization options with *programming code* or *xml files*.

### 1. Create IdenfyUISettings

Create an instance of IdenfyUISettings class:

#### V2
##### Java
```java
    IdenfyUISettingsV2 idenfyUISettingsV2 = new 
    IdenfyUISettingsV2.IdenfyUIBuilderV2()
    .build();
```
#### V1
##### Java
```java
    IdenfyUISettings idenfyUISettings = new 
    IdenfyUISettings.IdenfyUIBuilder()
    .build();
```

### 2.Update IdenfyUISettings
#### V2
##### Java
```java
    IdenfySettingsV2 idenfySettingsV2 = new IdenfySettingsV2.IdenfyBuilderV2()
    .withIdenfyUISettingsV2(idenfyUISettingsV2)
    ...
    build();
```
#### V1
##### Java
```java
    IdenfySettings idenfySettings = new IdenfySettings.IdenfyBuilder()
    .withUISettings(idenfyUISettings)
    ...
    build();
```

## Customization V1

iDenfy SDK groups various components and enable different customization options.

 ### *  Back navigation components

`idenfy_camera_session_back_navigation.xml` provides full customization via XML.

**Colors**

|Color name              |Description                     |
|-------------------|-------------------------------|
|`idenfyDocumentsCameraSessionBackArrowColor`   |Defines the color of the back arrow, inside of documents camera session view.                        |
|`idenfyDocumentsResultsBackArrowColor`|Defines the color of the back arrow, inside of documents result view.                    |
|`idenfyFaceSessionCameraBackArrowColor`  |Defines the color of the back arrow, inside of selfie camera session view.                     |
|`idenfyFaceResultsCameraBackArrowColor`  |Defines the color of the back arrow, inside of selfie result view.                    |

*Same pattern applies with text near the back icon.

### *  Loading view

 Setting different progress indicator for custom results layout.
```java
    IdenfyUISettings.IdenfyUIBuilder()
    withCustomLoadingView(Integer drawableId)
    ...
```
### *  ActionBarLayout

Removing actionBarLayout from UI. Helps to easier customize UI.
```java
    IdenfyUISettings.IdenfyUIBuilder()
    withAppBarLayoutEnabled(boolean isActionBarEnabled)
    ...
```
### *  Typeface of UI elements

Setting custom typeface for all UI elements.
```java
    IdenfyUISettings.IdenfyUIBuilder()
    withTypefacePath(String pathOfTypeface)
    ...
```

## Customization V2

SDK currently supports three ways of customization:
### Customization with IdenfyUISettingsV2:
#### * Confirmation view

```java
    IdenfyUISettings.IdenfyUIBuilder()
     /**
     * Confirmation View acts as additional step, which helps user to familiarize himself with identification process
     * @param isConfirmationViewNeeded Enables/Disables confirmation view
     */
    withConfirmationView(Boolean isConfirmationViewNeeded)
    ...
```
#### * Language selection
```java
    IdenfyUISettings.IdenfyUIBuilder()
    /**
     * Enables language selection window, which provides option to change locale
     * @param isLanguageSelectionNeeded Changes visibility of locale selection
     icon.
    */
    withLanguageSelection(Boolean isLanguageSelectionNeeded)
    ...
```
### Customization with styles.xml or colors.xml:
Every screen in SDK uses different styles.xml, which covers all UI elements visible in that screen. 

By overriding styles or colors in your own app target, you can change the look of IdenfySDK to match your brand guidelines.
You can access our styles.xml and colors.xml [here](https://github.com/idenfy/Documentation/blob/master/resources/sdk/android/).

### Customization with overriding layouts of SDK:
All layouts in iDenfySDK are structured in a way that it is easy to override all components to match your brand identity. Requirements for overriding layouts:
#### * Do not remove ids of components
This will lead to better project maintainability and will not cause runtime crashes.
#### * Keep same layouts name
If layouts names are changed, then layouts in SDK will not be overridden.

All layouts can be found [here](https://github.com/idenfy/Documentation/blob/master/resources/sdk/android/layouts/).

### Adding instructions in camera session.
iDenfySDK provides informative instructions during identification session. They can provide valuable information for the user and help to tackle common issues: bad lightning, wrong document side and etc. Instructions can be customized, by changing all UI elements or even using your own MP4 video files.
#### 1. Enable instructions in IdenfyUISettingsV2
 ```java
   IdenfyUISettingsV2 idenfyUISettingsV2 = new IdenfyUISettingsV2.IdenfyUIBuilderV2()
                .withInstructions(true)
                .build();
```

### Customization with using your own Fragments:
Coming soon... Stay tuned!



## Liveness customization V1

iDenfy SDK provides additional liveness customization.

### 1. Creating IdenfyLivenessUIHelper
#### V2
##### Java
 ```java
    IdenfyLivenessUISettingsV2 idenfyLivenessUISettingsV2 = new IdenfyLivenessUISettingsV2();
```

#### V1
##### Java
 ```java
    IdenfyLivenessUISettings idenfyLivenessUISettings = new IdenfyLivenessUISettings();
```
### 2. Applying settings
#### V1, V2
 **IdenfyLivenessUISettings** has following attributes for liveness customization
##### Kotlin
 ```Kotlin
    var livenessFeedbackBackgroundColor: Int? = null
    var livenessFeedbackFont: Typeface? = null

    //Liveness session frame settings
    var livenessFrameBackgroundColor: Int? = null
    var livenessFrameColor: Int? = null
    var livenessFrameWidth: Int? = null

    //Liveness session progress settings
    var livenessIdentificationOvalProgressColor1: Int? = null
    var livenessIdentificationOvalProgressColor2: Int? = null
    var livenessIdentificationProgressStrokeWidth: Int? = null
    var livenessIdentificationProgressRadialOffset: Int? = null
    var livenessIdentificationProgressStrokeColor: Int? = null

    //Liveness session overlay settings
    var livenessOverlayBrandingImage: Int? = null

    //Liveness ready screen settings
    var livenessReadyScreenForegroundColor: Int? = null
    var livenessReadyScreenBackgroundColor: Int? = null
    var livenessReadyScreenTextBackgroundColor: Int? = null
    var livenessReadyScreenButtonBorderColor: Int? = null
    var livenessReadyScreenButtonBorderWidth: Int? = null
    var livenessReadyScreenButtonCornerRadius: Int? = null
    var livenessReadyScreenButtonBackgroundNormalColor: Int? = null
    var livenessReadyScreenButtonBackgroundHighlightedColor: Int? = null
    var livenessReadyScreenButtonBackgroundDisabledColor: Int? = null
    var livenessReadyScreenShowBrandingImage: Boolean? = true

    //Liveness result screen settings
    var livenessResultScreenForegroundColor: Int? = null
    var livenessResultScreenIndicatorColor: Int? = null
    var livenessResultScreenUploadProgressFillColor: Int? = null
    var livenessResultScreenUploadProgressTrackColor: Int? = null
    var livenessResultScreenShowUploadProgressBar: Boolean? = true
    var livenessResultScreenResultAnimationSuccessBackgroundImage: Int? = null

    //Full custom settings
    var livenessCustomUISettings: com.facetec.zoom.sdk.ZoomCustomization?=null
```

### 3. Updating IdenfyUISettings
#### V1
##### Java
```java
    IdenfyUISettings idenfyUISettings = new IdenfyUISettings.IdenfyUIBuilder().
    withLivenessUISettings(idenfyLivenessUISettings).
    ...
```

#### V2
##### Java
```java
    IdenfyUISettingsV2 idenfyUISettingsV2 = new IdenfyUISettingsV2.IdenfyUIBuilderV2().
    withLivenessUISettings(idenfyLivenessUISettingsV2).
    ...
```

## Liveness customization V2
 iDenfySDK provides the following attributes for liveness customization:




