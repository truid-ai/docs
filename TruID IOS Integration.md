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
    curl --location --request POST 'https://release-api.truid.ai/generate-token/'  --header 'Authorization: Api-Key HEbOWwoI.aPiDjrvQqNa7M6YpT7VE4skxoMS4Eaxx'
    ```
    Ideally this api call should be performed on your serverside and here it should be calling the server to keep the api key safe

    




