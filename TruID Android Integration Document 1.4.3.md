# TruID Android Integration Document

You need to perform the following steps. 

1. Add it in your root build.gradle at the end of repositories:

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
                implementation 'com.github.truid-ai.TruId-Android:sdk:1.4.3'
                //for networking
                implementation 'com.amitshekhar.android:android-networking:1.0.2'
    
            }
    ```

3. Enable jettfier in gradle.properties
    ```javascript
    android.enableJetifier=true
    ```

4. Generate token using your API Key. Ideally this step should be performed on serverside. Here is a java snippet to give the idea of how to do it.
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
    Ideally this api call should be performed on your serverside and here it should be calling the server to keep the api key safe

5. Implement a result callback in your  activity

    ```kotlin
    private val authenticateUser = registerForActivityResult(AuthenticateWithTruID()) {
      Toast.makeText(
        this,
        "Session ID: ${it.sessionID}, Status: ${it.verificationStatus}, Error: ${it.error}",
        Toast.LENGTH_LONG).show()
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

    

6. Launch the activity by passing the generated token in it

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
                    authenticateUser.launch(AuthenticateWithTruID.Input(
                         token = token,
                         enableFaceLiveness = true,
                         enableOnDeviceLiveness = true,
                         enableDocumentCapture = true,
                         enableExtractData = true,
                         enableDocumentAuthenticity = true,
                         enableDocumentBacksideCapture = false,
                         enableIDtoSelfieMatching = true,
                         enableVerisysVerification = false,
                         enableFingerSelection = false,
                         enableFingerprintCapture = true,
                         enablePersonalInformationVerification = false,
                         enableMobileNumberVerification = false,
                         enableUndertaking = false,
                         enableAccountOptions = false,
                         enableAgentVerification = false
                     ))
   
                   },
       onError = { error ->
                  ...
                  //handle errors here
                 }
     )
   }
   ```

