# TruID Android Integration Document

You need to perform the following steps. 

1. Add it to your root build.gradle at the end of repositories:

    ```css
    allprojects {
        repositories {
            ...
            jcenter()
            maven { url 'https://jitpack.io' }
        }
    }
    
    ```

2. Add the dependency
    ```css
            dependencies {
                implementation 'com.github.truid-ai:android-sdk:1.1.2'
                //for networking
                implementation 'com.github.amitshekhariitbhu.Fast-Android-Networking:android-networking:1.0.4'
    
            }
    ```

3. (Optional) You can enable native libs extraction for smaller apk sizes. 
    ```xml
    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:extractNativeLibs="true">
        ...
    </application>
    ```

4. Enable jettfier in gradle.properties
    ```javascript
    android.enableJetifier=true
    ```

4. Generate token using your API Key. Ideally, this step should be performed on the server side. Here is a Kotlin snippet to give an idea of how to do it.
    ```kotlin
    private fun generateToken(
      apiKey: String,
      onSuccess: ((token: String) -> Unit),
      onError: ((error: String) -> Unit)
    ) {
      val defaultErrorMessage = "Error while generating token."
    
        AndroidNetworking.post("https://release-api.truid.ai/generate-token/")
        .addHeaders("Authorization", "Api-Key $apiKey")
        .setTag("get-token")
        .setPriority(Priority.HIGH)
        .build()
        .getAsJSONObject(object: JSONObjectRequestListener {
          override fun onResponse(response: JSONObject?) {
            val token = response?.getString("token")
    
              if (token == null) onError(defaultErrorMessage)
                else {
                  Log.i(TruID.LOG_TAG, "API Token: $token")
                    onSuccess(token)
                }
          }
    
          override fun onError(anError: ANError?) {
            onError(anError?.errorBody ?: defaultErrorMessage)
          }
        })
    }
    ```
    Ideally, this api call should be performed on your serverside and here it should be calling the server to keep the API key safe

5. Implement a result callback in your  activity

    ```kotlin
    private val authenticateUser = registerForActivityResult(AuthenticateWithTruID()) { result ->
      Toast.makeText(
        this,
        "Session ID: ${result.sessionID}, Status: ${result.verificationStatus}, Error: ${result.error}",
        Toast.LENGTH_LONG).show()
        //result.errror is a String that contains error messages if any error occurs while the SDK is running. some of the error messages are:
        //'Error while creating session'
        //'Configuration not found while creating session'
        //'Api not initialized'
    	//getting verification data here
      AndroidNetworking.get("https://release-api.truid.ai/sessions/${it.sessionID}/")
      .build()
      .getAsJSONObject(object: JSONObjectRequestListener {
        override fun onResponse(response: JSONObject?) {
          Log.d("----main app----", response.toString())
          //displaying verification data here
          Toast.makeText(applicationContext,response.toString() , Toast.LENGTH_LONG).show()
          var viewableText = "";
          if (response != null) {
            viewableText = "response: ${response}"
          }
          textView.text = viewableText
        }
    
        override fun onError(anError: ANError?) {
          Log.d("----- main app----", anError.toString())
        }
      })
    }
    ```

    

6. Launch the activity by passing the generated token into it

   ```kotlin
   fun launchTruID(){
     generateToken( //calling the function created in previous step
       apiKey = "<API Key goes here>",
       onSuccess = { token ->
                    //setting theme color here
                    TruID.setThemeColor(96, 22, 235)
                    TruID.setPassedColor(21, 255, 161)
                    TruID.setFailedColor(249, 78, 78)
                    //passing token and configuring what steps to run here
                    authenticateUser.launch(
            AuthenticateWithTruID.Input(
                token = token,
                enableFaceLiveness = false,
                enableOnDeviceLiveness = false,
                enableDocumentCapture = false,
                enableExtractData = false,
                enableDocumentAuthenticity = false,
                enableDocumentBacksideCapture = false,
                enableIDtoSelfieMatching = false,
                enableVerisysVerification = false,
                enableFingerSelection = false,
                enableFingerprintCapture = true,
                enablePersonalInformationVerification = false,
                enableMobileNumberVerification = false,
                enableUndertaking = false,
                enableAccountOptions = false,
                enableAgentVerification = false,
                displayHelpScreens = true,
                fingerprintOptions = FingerprintOptions(
                    fingersToScan = FingersToScan.LEFT_4,
                    minimumNIST = 40,
                    displayFingerprintResults = false
                ),
                enableReportScreen = true,
                disableLocationCapture = false,
            )
        )
   
                   },
       onError = { error ->
                  ...
                  //handle errors here
                 }
     )
   }
   ```

You can also optionally enable or disable specific steps by passing boolean values. Furthermore you can disable help screens by passing false to the disableHelpScreen parameter.

If you are using the fingerprint detection feature you can specify fingerprint options by passing it a FingerprintOptions object which takes the following parameters
1. fingersToScan: Specify the fingers you want to scan. The options are RIGHT_THUMB, RIGHT_4_FINGERS, RIGHT_HAND, LEFT_THUMB, LEFT_4_FINGERS, LEFT_HAND. We assume you have passed false to the enableFingerSelection parameter to only allow the user to scan the specified fingers.
2. minimumNIST: The minimum NIST score. The user is prompted to retry if the scan is of a lower quality than what was specified
3. displayFingerprintResults: If set to true the user is shown the scan results before they move on to the next step

## Integration for Flutter
### Setting up Method Channels

To set up method channels for communication between Flutter and Kotlin, follow these steps:

1. Create a new method channel object in both Flutter and Kotlin code.

```
 static const platform = MethodChannel('samples.flutter.dev/truIdSDK');

```
2. Define the method calls for each channel and the corresponding callbacks.
3. Use the `invokeMethod()` function to call methods from one codebase to the other.

```
  try {
      final int result = await platform.invokeMethod('launchTruID');
    } on PlatformException catch (e) {
      print(e);
    }
```
4. On the native side, this is the code to be added
```
    private val CHANNEL = "samples.flutter.dev/truIdSDK"

    override fun configureFlutterEngine(@NonNull flutterEngine: FlutterEngine) {
        super.configureFlutterEngine(flutterEngine)
        MethodChannel(flutterEngine.dartExecutor.binaryMessenger, CHANNEL).setMethodCallHandler {
            // This method is invoked on the main thread.
                call, result ->
            if (call.method == "launchTruID") {
                launchTruID()
                result.success("Success")
            } else {
                result.notImplemented()
            }
        }
    }

```


### Adding TruID SDKs

To add the TruID SDKs to the app, follow these steps:

1. Add the necessary dependencies and configurations for the TruID SDKs in the Gradle files.

```
  dependencies {
    implementation 'com.github.truid-ai:android-sdk:1.1.2'
    implementation 'com.github.amitshekhariitbhu.Fast-Android-Networking:android-networking:1.0.4'
}

```

### Handling MultiDex(in case it occurs)

To handle MultiDex, follow these steps:

1. Enable MultiDex in the Flutter project by adding the necessary dependencies and configurations to the Gradle files.

```
    dependencies{
      implementation 'com.android.support:multidex:1.0.3'
    }
```

2.In the `app.gradle` file, enable MultiDex by adding the following line to the `defaultConfig` section:

```
  defaultConfig {
    multiDexEnabled true
  }
``` 

### Flutter Activity Issue
2. Use the `FlutterFragmentActivity` instead of `FlutterActivity` to enable embedding the Flutter view into an existing Android view hierarchy.

To handle the Flutter activity issue, follow these steps:

```
class MainActivity : FlutterFragmentActivity() {
    ...
}   
```
By following these steps, you should be able to integrate the Flutter and Kotlin codebases using method channels for seamless communication and add the necessary TruID SDKs to authenticate and authorize users.

