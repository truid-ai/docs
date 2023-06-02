
# truID_FingerSDK Integration

1. Add the following package dependecies to your project:
https://github.com/truid-ai/T5AirSnapPackage.git version 0.1.0\
https://github.com/truid-ai/truID_FingerSDK.git version 0.4.0\
Alamofire version 5.7.1 (for networking)

2. Add the following code to where you want to call the SDK:

``` swift:

        truID_FingerSDK.GlobalSettings.API_URL = "https://release-api.truid.ai" //you server link here
        truID_FingerSDK.GlobalSettings.chosenColor = .blue
        let storyboard = UIStoryboard(name: "FingerprintCapture", bundle: Bundle(identifier: "ai.truid.truID-FingerSDK"))
        let controller = storyboard.instantiateViewController(withIdentifier: "SplashScreen") as! SplashScreen
        
        controller.modalPresentationStyle = .fullScreen // Set modal presentation style to full screen

        controller.token = "your token here"
        controller.API_URL = GlobalSettings.API_URL
        controller.session = 0
        controller.chosenColor = GlobalSettings.chosenColor
        controller.fingerprintCaptureDelegate = FingerCaptureDelegate(resultCallback: {SessionResult in
            print("Session ID in main app \(SessionResult.sessionID), Session status in main app \(SessionResult.status), Session Error in main app \(SessionResult.error)")
        }, errorCallback: {error in
            print("Errror in main app \(error)")
        })
        controller.modalPresentationStyle = .fullScreen // Set modal presentation style to full screen
        controller.overrideUserInterfaceStyle = .light
        controller.locationState = GlobalState()
        present(controller, animated: true)
```

Session id and status will be returned in the FingerCaptureDelegate resultCallback.

