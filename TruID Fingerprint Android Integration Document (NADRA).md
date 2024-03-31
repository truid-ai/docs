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
               implementation 'com.github.truid-ai.TruId-Android:sdk:6.0.3'
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
            this,
            "LivenessStatus: ${it.biometricData.fingerLiveness}, Error: ${it.error}",
            Toast.LENGTH_LONG
        ).show()
        //biometric output here
        Log.d("Truid_sdk", "cnic Number from sdk: ${it.biometricData!!.cnicNumber}")
        Log.d("Truid_sdk", "left finger index wsq: ${it.biometricData!!.leftIndexWSQ}")
        Log.d("Truid_sdk", "right finger index wsq: ${it.biometricData!!.rightIndexWSQ}")
   }
   ```

5. Launch the activity by passing the generated token in it

   ```kotlin
   fun launchTruID(){
        authenticateUser.launch(
            AuthenticateWithTruID.Input(
                enableFingerSelection = true,
                displayHelpScreens = true,
                enableFingerLiveness = true,
                fingerprintOptions = FingerprintOptions(
                    fingersToScan = FingersToScan.LEFT_HAND,
                    minimumNIST = 40,
                    captureCnic = true,
                )
            )
        )
   }
   ```
