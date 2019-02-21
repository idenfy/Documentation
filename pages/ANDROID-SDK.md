## Table of contents

*   [Getting started](#getting-started)
*   [Callbacks](#callbacks)
*   [Customising flow](#customising-flow)
*   [UI Customisation](#ui-customisation)
*   [Advanced Liveness detection](#advanced-liveness-detection)

## Getting started
The SDK supports API Level 15 and above

Our current gradle configuration supports newest support library:

`targetSdkVersion = 28`

`compileSdkVersion = 28`

`buildToolsVersion '28.0.3'`


### 1. Obtaining token
SDK requires token for starting initialization. [Token generation guide](https://github.com/idenfy/Documentation/blob/master/pages/GeneratingIdentificationToken.md)

### 2. Adding the SDK dependency
In the root level (project module) gradle add following implementation:

```gradle
repositories {
  ...
  maven {
    url  "https://dl.bintray.com/idenfy/idenfy"
  }
}
```
In the app level gradle add following implementation:
```gradle
repositories {
  ...
  dependencies {  
      implementation 'idenfySdk:com.idenfy.idenfySdk:+' 
    }
}
```
*Note: All new versions will support backwards compatibility.
### 3. Enabling Java 8 support
It is required to enable Java 8 support, if it was already not provided:
```gradle
 compileOptions {
        targetCompatibility 1.8
        sourceCompatibility 1.8
    }
```

### 4. Configuring SDK
It is required to provide following configuration:
### Java
```java
IdenfySettings idenfySettings = new IdenfySettings.IdenfyBuilder()
                .withAuthToken("AUTH_TOKEN")
                .build();
```


### 5. Presenting Activity
Instance of IdenfyController is required for starting a flow.

### Java
```java
   IdenfyController.getInstance().startActivityForResult(context, IdenfyController.IDENFY_REQUEST_CODE, idenfySettings);
   //context must be of a activity type
```
## Callbacks
SDK provides following callbacks: onSuccess, onError and onUserExit.

It is required to override onActivityResult for receiving responses.

### Java
```java
    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if (requestCode == IdenfyController.IDENFY_REQUEST_CODE) {

            if (resultCode == IdenfyController.AUTHENTICATION_RESULT_CODE) {
                AuthenticationResultResponse authenticationResultResponse = data.getParcelableExtra(IdenfyController.ON_AUTHENTICATION_RESULT);
            } else if (resultCode == IdenfyController.ERROR_CODE) {
                IdenfyErrorResponse idenfyErrorResponse = data.getParcelableExtra(IdenfyController.ON_ERROR);
                //Error response
            } else if (resultCode == IdenfyController.USER_EXIT_CODE) {
                //User exited the SDK
            }
            
        }
    }
```


[Additional information about callbacks](https://github.com/idenfy/Documentation/blob/master/pages/StandardErrorMessages.md)

## Customising flow
 SDK provides various options for changing identification flow. All requirements can be specified inside of IdenfyBuilder()
 
 *Note: SDK provides Builder pattern to improve code testibility and maitanance. Equivalently setters can also be used.
 
 ### 1. Removing initial Fragment

If default document country was selected during **token generation** the terms of services and country information View can be removed.
```java
   IdenfySettings.IdenfyBuilder()
    .withPresentInitialView(false)
    ...
```

### 2. Setting custom results view

If results view UI is not suitable for your design we provide customisation. We provide full xml file of results view
```java
   IdenfySettings.IdenfyBuilder()
    .withCustomResultsView(true)
    ...
```

### 3. Custom locale

 By default SDK provides following translations:

 - English (en) GB
 - Polish (es) PL
 - Russian (es) RU
 - Lithuanian (es) LT

The language of SDK is selected by the language configurations of the **device**. In order to setup custom localization the following method must be called
```java
   IdenfySettings.IdenfyBuilder()
    .withCustomSelectedLocale("locale")
    ...
```
## UI Customisation

SDK provides various ways of changing UI for better design integration.
 ### 1. UI settings

### Java
```java
IdenfyUISettings idenfyUISettings = new 
IdenfyUISettings.IdenfyUIBuilder()
    .build();
```
 ### 2. Customisable features
 Setting different progress indicator for custom layout
```java
IdenfyUISettings.IdenfyUIBuilder()
    withCustomLoadingView(Integer drawableId)
    ...
```
Removing actionBarLayout from UI. Helps to easier customize UI.
```java
IdenfyUISettings.IdenfyUIBuilder()
    withAppBarLayoutEnabled(boolean isActionBarEnabled)
    ...
```

For setting custom typeface.
```java
IdenfyUISettings.IdenfyUIBuilder()
    withTypefacePath(String pathOfTypeface)
    ...
```
Colors can be easily changed by overriding values of the colors.xml in the app module

`idenfyColorPrimary`: Sets most attributes in the UI.

`idenfyColorPrimaryDark`: Sets the background color of the`Toolbar`

`idenfyColorAccent`: Sets the color of button, checkboxes, icons.

`idenfyNextButtonColor`: Defines the color of the next button, inherits from idenfyColorAccent by default.

More than 20 other color customisations available within SDK.


 ## Advanced Liveness detection
IdenfySDK provides advanced liveness recognition. Liveness recognition is attached as separate, optional module inside of the SDK. 
 
Attached liveness SDK will sync with **core** Idenfy SDK.

In the app level gradle add following implementation:
```gradle
repositories {
  ...
  dependencies {  
      implementation 'idenfySdk:com.idenfy.idenfyliveness:+' 
    }
}
```
 
*Note: Contact support for enabling liveness SDK






