
<h2>Getting Started</h2>

If you haven't installed the SDK yet, please [go to our quickstart guide](/quickstart) to get our SDK up and running in Xcode. Note that we support iOS 8.0 and higher, and React Native v0.7.0 and higher. If you're interested in more detailed information about our SDK, you can check out our <a href='/api/ios' target='_blank'>full API reference</a>.

Once you have installed the AppHub SDK, you can update your React Native JavaScript code and images by uploading new Xcode builds (IPAs) to the AppHub dashboard. Our SDK will  look for new builds and automatically update your users' apps.

On AppHub, you create an App for each of your mobile applications. Each App has its own application id that you will use to configure the SDK. Each of your Apps will contain multiple Builds of your mobile application. You can configure and deploy Builds to your users from the AppHub dashboard.

---

<h3 short-title='Components'>Native and JavaScript components</h3>

All AppHub developers should understand the distinction between React Native "native components" and JavaScript components. Every React Native application contains both native code (Objective-C/Swift) and JavaScript. You will likely be making most of your changes to JavaScript code, and you will make occasional modifications to native code.

AppHub allows you to push JavaScript and image updates to your users. **If you make breaking changes to native code, you must update your iOS application via Apple**.

We highly recommend that you test your AppHub builds with their associated native code versions
before deploying to your users. Check out the [testing section](#docs-testing-builds) to learn more.

---

<h3 short-title='Basic Configuration'>Basic SDK Configuration</h3>

This section describes the most basic AppHub configuration that will allow you to push changes to JavaScript code and images.

First, include our SDK libraries from your `AppDelegate.m` file:

    #import <AppHub/AppHub.h>

Then, add this line to the beginning of your  `application:didFinishLaunchingWithOptions:` method in the `AppDelegate.m` file, replacing `Application ID` with the application id from the AppHub dashboard:

    [AppHub setApplicationID:@"Application ID"];

Finally, use `[AppHub buildManager].currentBuild` to get the most up-to-date build. Then use `build.bundle` (type `NSBundle` to access the `main.jsbundle` file (or any other `.jsbundle` file in your build):

    AHBuild *build = [AppHub buildManager].currentBuild;
    NSURL *jsCodeLocation = [build.bundle URLForResource:@"main"
                                           withExtension:@"jsbundle"];


As is standard for React Native apps, initialize an `RCTRootView` with this `jsCodeLocation` and present the view.


The AppHub SDK will automatically update the `currentBuild` with the appropriate build, as configured from the AppHub dashboard.

---

<h3 short-title='Listening for New Builds'>Listening for New Builds</h3>

If you want to perform an action when a new build becomes available to your application, such as displaying an alert to the user or force refreshing the app, you can listen for new build events.

From Objective-C you can list for notifications with the string `AHBuildManagerDidMakeBuildAvailableNotification`.

From JavaScript you can register a listener for this event like so:

    var { NativeAppEventEmitter } = React;
    var subscription = NativeAppEventEmitter.addListener(
      'AppHub.newBuild',
      (build) => {
        // Show a modal, alert the user, etc...
      }
    );

---

<h3 short-title='Testing Builds'>Testing Builds</h3>

We recommend that you test new builds on the version that is running in the App Store. To do this, checkout the version of your app that you submitted to the App Store and use the build selector to test builds:

    // Create a root view controller and present it...

    [AppHub presentSelectorOnViewController:vc
                           withBuildHandler:^(AHBuild *result, NSError *error) {
      NSURL *jsCodeLocation = [result.bundle URLForResource:@"main"
                                              withExtension:@"jsbundle"];
      // Now initialize an RCTRootView with this bundle.
    }];

---

<h3 short-title='Polling for New Builds'>(Advanced) Polling for New Builds</h3>

The AppHub SDK will poll our servers for new builds of your App. To avoid interfering with your mobile application's normal operation, the SDK will only poll during app inactivity.


If you wish to manually control the frequency and timing of the polling, you can disable automatic polling:

    [AppHub buildManager].automaticPollingEnabled = NO;

To poll for new builds, call this method:

    [[AppHub buildManager] fetchBuildWithCompletionHandler:nil];

Check out the <a href='/api/ios' target='_blank'>full API reference</a> for more ways to poll for builds, including methods for callbacks and synchronous fetching of builds.
