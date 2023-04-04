## Introduction
This documentation provides an overview of the app and its components. The app is built using Flutter for the front-end and Kotlin for the back-end.

## Requirements
The following are the requirements for building and running the app:
- Flutter 3.0 or higher 
- Kotlin 1.6 or higher 
- Gradle Version 7.5 or higher 

## Installation 
To install the app, follow the steps below:
1. Clone the repository from [insert link to the repository].
2. Open the entire Flutter project in a text editor like Visual Studio Code.
3. Open the android folder only in Android Studio, as it will sync the Gradle automatically.
4. The application can be run using Android Studio or VS Code using the command `flutter run` or the run button in Android Studio.

## Code Structure
The app code is organized as follows:
- `lib` folder contains the Flutter front-end code
- `kotlin` folder contains the native Kotlin code
- The `app.build.gradle` file has all the app-specific dependencies in it.
- The `android.build.gradle` has all the Android-specific dependencies.
- The `pubspec.yaml` file has the Flutter-specific dependencies.

## Dependencies Installation
These dependencies are required to run the app. To be installed in the `app.gradle` file, in the dependencies section:

```
  dependencies {
    implementation "org.jetbrains.kotlin:kotlin-stdlib-jdk7:$kotlin_version"
    implementation 'com.github.truid-ai.TruId-Android:sdk:1.7.1-slim'
    implementation 'com.amitshekhar.android:android-networking:1.0.2'
    implementation 'com.an  droid.support:multidex:1.0.3'
    
}

```
In the android build gradle section, the repositories section should look something like this

```

allprojects {
    repositories {
        google()
        jcenter()
        maven { url 'https://jitpack.io' }
    }
}

```

## Integration Process

The integration process involves combining the Flutter front-end code with the Kotlin back-end code using method channels. This allows for seamless communication between the two codebases.

### 1. Setting up the Flutter Project

To set up the Flutter project, follow these steps:

1. Create a new Flutter project using Flutter CLI or IDE.
2. Add the necessary dependencies for the app, including the `flutter_channel` package for communication between Flutter and Kotlin.
3. Create the necessary screens and widgets for the front-end of the app.

### 2. Setting up the Kotlin Project

To set up the Kotlin project, follow these steps:

1. Create a new Kotlin project using the appropriate IDE or build system.
2. Add the necessary dependencies for the app, including the `kotlinx_coroutines` package for asynchronous communication.
3. Create the necessary classes and functions for the back-end of the app.

### 3. Setting up Method Channels

To set up method channels for communication between Flutter and Kotlin, follow these steps:

1. Create a new method channel object in both Flutter and Kotlin code.
2. Define the method calls for each channel and the corresponding callbacks.
3. Use the `invokeMethod()` function to call methods from one codebase to the other.

### 4. Adding TruID SDKs

To add the TruID SDKs to the app, follow these steps:

1. Clone the private repository containing the TruID SDKs.
2. Add the necessary dependencies and configurations for the TruID SDKs in the Gradle files.
3. Use the TruID APIs to authenticate and authorize users in the app.

### 5. Handling MultiDex and Activity Issues

To handle MultiDex and activity issues, follow these steps:

1. Enable MultiDex in the Flutter project by adding the necessary dependencies and configurations to the Gradle files.
2. Use the `FlutterFragmentActivity` instead of `FlutterActivity` to enable embedding the Flutter view into an existing Android view hierarchy.

By following these steps, you should be able to integrate the Flutter and Kotlin codebases using method channels for seamless communication and add the necessary TruID SDKs to authenticate and authorize users.


## Troubleshooting
The following are common issues that may arise when building or running the app and how to resolve them:
1. Be sure to install all dependencies before running the file.
2. Make sure to sync Gradle after making any changes.
3. Make sure to have an internet connection when building the app to download the necessary Flutter, Kotlin, Gradle, and TruID dependencies.
4. Run the following commands before running the project:
    ```
    flutter clean
    flutter pub get
    ```

## Conclusion
This documentation provides an overview of the app, its requirements, installation, configuration, usage, code structure, components, and troubleshooting. By following these instructions, users should be able to build and run the app with ease.
