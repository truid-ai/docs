# TruID Android Integration Document

You need to perform the following steps.

1. Add it in your root build.gradle at the end of repositories:

   ```gradle
   allprojects {
       repositories {
           ...
           jcenter()
           maven { url 'https://jitpack.io' }
       }
   }

   ```

2. Add the dependency

   ```gradle
           dependencies {
               implementation 'com.github.truid-ai.TruId-Android:sdk:6.0.2'


           }
   ```

3. Enable jettfier in gradle.properties

   ```gradle
   android.enableJetifier = true;
   ```

4. Implement a result callback in your activity

   ```kotlin
   private val authenticateUser = registerForActivityResult(AuthenticateWithTruID()) {
        Toast.makeText(
            this, "status: ${it.verificationStatus} Error: ${it.error}", Toast.LENGTH_LONG
        ).show()
        //verificationStatus: either the face presented was live or not
        //faceImageBitmap: return the captured face image in Bitmap
        Log.d("Truid_sdk", "face b64: ${it.faceImageBitmap!!}")
   }
   ```

5. Launch the activity

   ```kotlin
   fun launchTruID(){
        authenticateUser.launch(
            AuthenticateWithTruID.Input(
                displayHelpScreens = true,
            )
        )
   }
   ```
