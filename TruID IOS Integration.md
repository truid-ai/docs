# TruID IOS Integration Document.

You need to perform the following steps in order to integrate 
1. Add the tech5 SDK and truID SDK to your project. The SDKs are available as swift packages. Add the folllowing swift packages in your projects.
    - TruID: https://github.com/truid-ai/TruIDPackag exact verion: 1.8.1
    - T5Airnap: https://github.com/truid-ai/T5AirSnapPackage exact version: 0.1.0
    - lottie-ios: https://github.com/airbnb/lottie-ios exact version: 3.4.0
    - Alamofile: https://github.com/Alamofire/Alamofire exact version: 5.6.2


    if you have any of these packages already installed in any other form (framework/cocoapods) you dont need to re-add them. The main aim is all of the frameworks should be present in the project.

    if you don't want to use swift package you can get the xcframework from these swift packages and add them manually in your project. 

2. Generate token using your API Key. Ideally this step should be performed on serverside. Here is a curl request to give the idea of how to do it.
    ```command
    curl --location --request POST 'https://release-api.truid.ai/generate-token/'  --header 'Authorization: Api-Key <API KEY HERE>'
    ```
    Ideally this api call should be performed on your serverside and here it should be calling the server to keep the api key safe

3. TruID SDK exposes a SwiftUI component which you can call and the flow starts working. The function takes input the generated token from previous step, some input parameters to customize the flow and callback functions for success and error. The extracted data is returned in these callback functions.
    ```swift
    TruidMain(
        token: "<TOKEN HERE>",
        API_URL: "https://release-api.truid.ai",
        face_liveness: false,
        document_capture: true,
        extract_data: false,
        document_authenticity: true,
        document_backside_capture: true,
        id_to_selfie_matching: false,
        fingerprint_capture: false,
        fingerprint_selection: false,
        verisys_verification: false,
        personal_information_verification: false,
        mobile_number_verification: false,
        undertaking: false,
        
        agent_verification: false,
        
        fingerprint_to_scan: .RIGHT_4,
        
        themeColor: Color(UIColor(red: 2/255, green: 131/255, blue: 203/255, alpha: 1.0)),
        
        success: { sessionResult in
            self.session = sessionResult
            self.token = nil
        },
        
        failure: { error in
            print(error)
            self.token = nil
            self.error = error
        },
        enableHelpScreens:true,
        enableReportScreen: true
    )
    ```




