## SDK Integration

The truID fingersdk is a component that needs to be integrated into the main application of the clients. For example, with Askari, we had to create an applet in **UIKit** as it is compliant with **iOS 13**. Swift UI cannot be used for this integration.

## Problems Faced

- Navigation in Storyboard: It is recommended to keep the navigation in the storyboard as dealing with it in code can lead to potential errors and screen size issues. Xcode does not support many old features of UIKit.
- Using Constraints: Learn how to use constraints in the storyboard for UI elements. However, for complex-shaped UI elements, it is better to handle them in code as it is more intuitive.

## Suggestions

- Incremental Changes in Storyboard: Avoid making big changes in the storyboard all at once, as Xcode can sometimes crash on undo. It is advisable to make incremental changes and test each step.
- Utilize Xcode Debugger: The Xcode debugger is a powerful tool that can help you troubleshoot issues and track down bugs. Familiarize yourself with its features and use it as your ally during development.
- Study Design Patterns: Familiarize yourself with various design patterns such as singleton, factory, and strategy. They can provide structure and maintainability to your codebase.
- Access Control: Keep all the classes in the SDK internal, as the main app should not have direct access to internal parameters. Only expose necessary interfaces to the main app.
- Suggested Roadmap: For me personally, i jumped in blind into UIKit. Thankfully most of the documentation for it is before 2021 which means it is available in the chatGPT dataset. You can ask it questions and it will always give upto date answers. 
- - Go into UIkit documentation. Its pretty straight forward stuff. Try not to use vanilla view controllers and use navigation controller.
- - Use contraint layouts with height and widths as percentages of the screen bounds so that your UI is adaptive.
- - Good Luck!

## Main Files

The following files are crucial in the project:

- `FingerprintCaptureViewController.swift`: This file represents the main screen in the SDK. Pay close attention to this file as it serves as the core of the fingerprint capture functionality.


- `PreviewScreenController.swift`: This file actually sets the relevant state of the fingerprint capture of the app. It stores it in the user defaults. Ideally this should be changed to be kept in the sdkSettings class as a static field for consistency

The applet should return the fingerprintresults back to the main app and the UI is to be separately handled in this case.

### Fix for handling UI stuck on last screen

Wrapped the initial screen of the sdk within a navigation controller which basically makes all the screens being pushed onto it into a stack. This way we can pop back to the root viewcontroller AKA back to the application.



