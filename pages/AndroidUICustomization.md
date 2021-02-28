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
#### * Adding instructions in camera session.
iDenfySDK provides informative instructions during identification session. They can provide valuable information for the user and help to tackle common issues: bad lightning, wrong document side and etc. Instructions can be customized, by changing all UI elements or even using your own MP4 video files.

Instructions are disabled by default on Android.

If you wish to override your configuration, you can always do it directly with IdenfyUISettingsV2.

Override instructions in IdenfyUISettingsV2:
 ```java
   IdenfyUISettingsV2 idenfyUISettingsV2 = new IdenfyUISettingsV2.IdenfyUIBuilderV2()
                .withInstructions(true)
                .build();
```

### Applying SDK wide color changes
If **color and assets changes** are the only requirement, then it can be easily customized by changing main colors.

Information about mostly used colors:

|Color name              |Description                     |Default color value
|-------------------|-------------------------------|------------------------------------
|`idenfyMainColorV2`   |Defines the color of most single colored assets and focused parts in SDK.                 |#536DFE
|`idenfyMainDarkerColorV2`|Defines the color of some focused parts in SDK, similar to idenfyMainColorV2.  |#5D7CE4
|`idenfyBackgroundColorV2`   |Defines the background color.            |#FBFBFB
|`idenfySecondColorV2`|Defines the text color.    |#F2353B4E
|`idenfyGradientAccentV2`   |Defines the second color of gradient. Currently used in confirmation buttons.                |#8D6CFB

You can customize it in a following manner:

#### 1. Override color names in your app module.
Create either a new idenfy_colors.xml or add our defined colors in your project.

#### 2. Make color changes
Example:
```xml
<resources>
    <color name="idenfyMainColorV2">#7CFC00</color>
    <color name="idenfyMainDarkerColorV2">#7CFC00</color>
</resources>
```

Colors also are applied on images, which use a single color from *idenfy drawable resources* .If perhaps you decided to override our provided images with more sophisticated icons, which use more than 1 color, then you can easily disable tint on images. You need to override our defined layouts styles with removed tint attribute.

Example:
### Before:
```xml
<style name="idenfyAppBarLayoutBackButtonStyle">
    <item name="android:tint">
        @color/idenfyMainColorV2
    </item>
</style>
``` 

### After:
```xml
<style name="idenfyAppBarLayoutBackButtonStyle" />
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
If layouts' names are changed, then layouts in SDK will not be overridden.

All layouts can be found [here](https://github.com/idenfy/Documentation/blob/master/resources/sdk/android/layouts/).

### Customization with skipping views
The SDK provides a set of tools to omit some views, which could be created in your application yourself offering a fine-grained approach. 
For example, you would like to implement document selection and the document's issuing country selection in the same view instead of having 2 separate.

*Note. 
All customization options listed below can be combined, e.g. you can skip both document selection, confirmation screen, and document issuing country selection.

#### * Skip document's issuing country selection screen.
##### 1. Generate an identification token with the provided document issuing country.
Take a look at [identification token generation documentation](https://github.com/idenfy/Documentation/blob/master/pages/GeneratingIdentificationToken.md#we-recommend).

Example of a JSON request body:
```json
{
   "clientId":"TEST_CLIENT_ID",
   "country": "lt"
}
```
##### 2. Contact support for enabling this feature.
Contact our tech support for enabling this feature to your account settings. Contact at techsupport@idenfy.com.

#### * Skip documents selection screen.
##### 1. Generate an identification token with the provided document type.
Take a look at [identification token generation documentation](https://github.com/idenfy/Documentation/blob/master/pages/GeneratingIdentificationToken.md#we-recommend).

Example of a JSON request body:
```json
{
   "clientId":"TEST_CLIENT_ID",
   "documents": ["PASSPORT"]
}
```
##### 2. Contact support for enabling this feature.
Contact our tech support for enabling this feature to your account settings. Contact at techsupport@idenfy.com.

#### * Skip document onboarding screen.
##### 1. Contact support for enabling this feature.
Contact our tech support for enabling this feature to your account settings. Contact at techsupport@idenfy.com.


## Liveness customization V1

iDenfy SDK provides additional liveness customization.

### 1. Creating IdenfyLivenessUIHelper
#### V1, V2
##### Java
 ```java
    IdenfyLivenessUISettings idenfyLivenessUISettings = new IdenfyLivenessUISettings();
```

### 2.1 Applying regular settings
If you only need color, text, or width customization, you can use properties from the IdenfyLivenessUISettings class.
#### V1, V2
#### IdenfyLivenessUISettings
##### Kotlin
 ```Kotlin
   class IdenfyLivenessUISettings() {

    //Liveness session feedback settings
    var livenessFeedbackBackgroundColor: Int? = null
    var livenessFeedbackFont: Typeface? = null

    //Liveness session frame settings
    var livenessFrameBackgroundColor: Int? = null
    var livenessFrameColor: Int? = null
    var livenessFrameWidth: Int? = null

    //Liveness session cancel button settings
    var livenessCancelButtonImage:Int?=null

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

    //Camera Permission
    var livenessCameraPermissionsScreenImage:Int?=null

    //Liveness result screen settings
    var livenessResultScreenForegroundColor: Int? = null
    var livenessResultScreenIndicatorColor: Int? = null
    var livenessResultScreenUploadProgressFillColor: Int? = null
    var livenessResultScreenUploadProgressTrackColor: Int? = null
    var livenessResultScreenShowUploadProgressBar: Boolean? = true
    var livenessResultScreenResultAnimationSuccessBackgroundImage: Int? = null

    //Liveness id check customization
    var livenessIdCheckCustomization = LivenessIdCheckCustomization()

    //Full custom settings
    var livenessCustomUISettings: com.facetec.sdk.FaceTecCustomization? = null
   }
```

#### LivenessIdCheckCustomization
##### Kotlin
```Kotlin
class LivenessIdCheckCustomization() {
        var buttonBackgroundNormalColor: Int?=null
        var buttonBackgroundHighlightColor: Int?=null
        var captureScreenTextBackgroundColor: Int?=null
        var reviewScreenTextBackgroundColor: Int?=null
        var captureFrameStrokeColor: Int?=null
    }
```

### 2.2 Applying full customization
If you require more changes, you can directly set **livenessCustomUISettings** property in the *IdenfyLivenessUISettings* with your own FaceTecCustomization. 

Full customization options are available [here](https://dev.facetec.com/ui-customization).
*Note 
It will override all other set properties of the IdenfyLivenessUISettings class.


### 3. Updating IdenfyUISettings
#### V1
##### Java
```java
    IdenfyUISettings idenfyUISettings = new IdenfyUISettings.IdenfyUIBuilder().
    withLivenessUISettings(idenfyLivenessUISettings).
    ...
    build()
```

#### V2
##### Java
```java
    IdenfyUISettingsV2 idenfyUISettingsV2 = new IdenfyUISettingsV2.IdenfyUIBuilderV2().
    withLivenessUISettings(idenfyLivenessUISettingsV2).
    ...
    build()
```




