## Table of contents

*   [Getting started](#getting-started)
*   [Customization of elements](#customization-of-elements)
*   [Liveness Customization](#liveness-customization)

## Getting started
Android SDK provides various customization options with code or xml

## Customization of elements
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

## Liveness Customization

iDenfy SDK provides additional liveness customization.

 ### 1. Creating IdenfyLivenessUIHelper

 ```java
 IdenfyLivenessUISettings idenfyLivenessUISettings = new IdenfyLivenessUISettings();
    ...
```
 ### 2. Applying settings

 Atrributes of IdenfyLiveness UISettings

 ```java
 //Allows you to change color of the feedback bar shown during Liveness
 idenfyLivenessUISettings.setLivenessFeedbackBackgroundColor(getResources().getColor(R.color.idenfyColorPrimaryDark));

// Color of the mainscreen, Pre-Enrollment, and Retry screens' background
 idenfyLivenessUISettings.setLivenessMainBackgroundColor(Integer integer);

// Color of the mainscreen, Pre-Enrollment, and Retry screens' foreground
 idenfyLivenessUISettings.setLivenessMainForegroundColor(getResources().getColor(R.color.idenfyColorPrimaryDark));

// Color of the background surrounding the oval outline during Liveness
 idenfyLivenessUISettings.setLivenessFrameBackgroundColor(getResources().getColor(R.color.idenfyColorPrimaryDark));

// Color of the animated 'progress spinner' strokes during Liveness
idenfyLivenessUISettings.setLivenessIdentificationOvalProgressColor1(getResources().getColor(R.color.idenfyColorPrimary));

idenfyLivenessUISettings.setLivenessIdentificationOvalProgressColor2(getResources().getColor(R.color.idenfyColorPrimary));

// Color of the outline of the oval during Liveness
idenfyLivenessUISettings.setLivenessIdentificationProgressStrokeColor(getResources().getColor(R.color.idenfyColorPrimary));

// Thickness of the outline of the oval during Liveness
idenfyLivenessUISettings.setLivenessIdentificationProgressStrokeWidth(14);

// Radial offset of the animated 'progress spinner' strokes relative to the outermost bounds of the oval outline. As this value increases, animations move closer toward the oval's center
idenfyLivenessUISettings.setLivenessIdentificationProgressRadialOffset(16);
```
 ### 3. Updating IdenfyUISettings

```java
 IdenfyUISettings idenfyUISettings = new IdenfyUISettings.IdenfyUIBuilder().
        ...
        withLivenessUISettings(idenfyLivenessUISettings).
                        build();
```





