<div  style="text-align:center"><img src="/puzzl-logo.png" alt="Puzzl" width="200"/></div>

# Welcome to Puzzl's iOS SDK
Puzzl iOS SDK for rendering Puzzl's Employee Onboarding flow

## Add Puzzl SDK to a project

### Using CocoaPods

1. You can use CocoaPods ("CocoaPods is an open source dependency manager for Swift and Objective-C Cocoa projects. CocoaPods makes it easy to install or update new SDKs when working with Xcode.") 

```bash
$ sudo gem install cocoapods
```

1. Create a Podfile in project directory (same directory as .xcodeproj file)
2. Open Podfile and include the PuzzlIOS dependency. An example is shown here: 

```bash
target "YourProjectNameHere" do
use_frameworks!
	pod 'puzzl-iOS', '1.7.0'
end
```

1. Run 'pod install' in directory of Podfile

```bash
$ pod install
```

1. To update the SDK at any time, run 'pod update' to get the most recent version of the Puzzl iOS SDK.
2. **After installation is done, use the newly created .xcworkspace file of your project.**

## Using the Puzzl iOS SDK

### Configure your app to work with the Veriff iOS SDK

1. **Add usage descriptions to application Info.plist**

> Not adding these usage descriptions causes system to kill application when it requests the permissions when needed.

Veriff iOS SDK requires camera and microphone permissions for capturing photos an video during identification. Your application is responsible to describe the reason why camera and microphone is used. You must add 2 descriptions listed below to `info.plist` of your application with the explanation of the usage.

- `NSCameraUsageDescription`
- `NSMicrophoneUsageDescription`

It should look like:

<div  style="text-align:center"><img src="/info_plist.png" alt="plist.info_file"/></div>



2. **Remove any references to the Scene Delegate**

You will need to delete your `SceneDelegate.swift` file and remove any references to the Scene Delegate in your `AppDelegate.swift` file. You will also need to instantiate just below your AppDelegate class definition. 

    ```swift
    var window:UIWindow?
    ```

### Add the Puzzl onboarding process

1. Import Puzzl into your code. In order to use the Puzzl SDK, import it in the class that will use the SDK (typically a View Controller).

    ```swift
    import Puzzl_iOS
    ```

2. In the place you want to trigger Puzzl's onboarding, set the delegate in order to follow the Puzzl Onboarding SDK status and allow Puzzl to show onboarding. Example:

    ```swift
    Puzzl.setDelegate(from: <YOUR VIEW CONTROLLER>)

    Example:

    Puzzl.setDelegate(from: self)
    ```
 

4. Call the 'showOnboardingWith' method from Puzzl. Example:

    ```swift
    Puzzl.setDelegate(from: <YOUR VIEW CONTROLLER>)
    Puzzl.showOnboarding(apiKey: <PUZZL LIVE KEY>,
                             companyID: <PUZZL COMPANY ID>,
                             workerID: <PUZZL EMPLOYEE ID>,
                             from: <YOUR VIEW CONTROLLER>)
    ```

5. To track the status of the Puzzl onboarding process, create a new method:

    ```swift
    extension ViewController: PuzzlDelegate {
        func getStatus(status: PuzzlStatus) {
            switch status {
            case .error:
                print("Error")
    						//handle error in onboarding
            case .success:						
                print("Success")
    						//handle successful onboarding
            }
        }
    }
    ```

    Once the worker onboards successfully, you can now run payroll for them! 🎉 
