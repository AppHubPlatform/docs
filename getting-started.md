
<h2>Getting Started</h2>

If you haven't installed the SDK yet, please [go to our quickstart guide](/quickstart) to get our SDK up and running in Xcode. Note that we support iOS 7.0+, and React Native v0.7.0 and higher. If you're interested in more detailed information about our SDK, you can check out our <a href='/api/ios' target='_blank'>full API reference</a>.

Once you have installed the AppHub SDK, you can update your React Native JavaScript code and images by uploading new Xcode builds (IPAs) to the AppHub dashboard. Our SDK will  look for new builds and automatically update your users' apps.

On AppHub, you create an App for each of your mobile applications. Each App has its own application id that you will use to configure the SDK. Each of your Apps will contain multiple Builds of your mobile application. You can configure and deploy Builds to your users from the AppHub dashboard.

---

<h3 short-title='Components'>Native and JavaScript components</h3>

All AppHub developers should understand the distinction between React Native "native components" and JavaScript components. Every React Native application contains both native code (Objective-C/Swift) and JavaScript. You will likely be making most of your changes to JavaScript code, and you will make occasional modifications to native code.

AppHub allows you to push JavaScript and image updates to your users. **If you make breaking changes to native code, you must update your iOS application via Apple**.

We recommend that you test your AppHub builds with their associated native code versions
before deploying to your users. Check out the [testing section](#docs-testing-builds) to learn more.

---

<h3 short-title='Basic Configuration'>Basic SDK Configuration</h3>

This section describes the most basic AppHub configuration that will allow you to push changes to JavaScript code and images.

First, include our SDK libraries from your `AppDelegate.m` file:

    #import <AppHub/AppHub.h>

Then, add this line to the beginning of your  `application:didFinishLaunchingWithOptions:` method in the `AppDelegate.m` file, replacing `Application ID` with the application id from the AppHub dashboard:

    [AppHub setApplicationID:@"Application ID"];

Finally, use `[AppHub buildManager].currentBuild` to retrieve the cached AppHub build. Then use `build.bundle` to access the `main.jsbundle` file:

    AHBuild *build = [AppHub buildManager].currentBuild;
    NSURL *jsCodeLocation = [build.bundle URLForResource:@"main"
                                           withExtension:@"jsbundle"];

As is standard for React Native apps, initialize an `RCTRootView` with this `jsCodeLocation` and present the view.

When you deploy new builds of your app with AppHub, the SDK downloads the new build
in the background and then loads from the cache at the next call to `[AppHub buildManager].currentBuild`.

If no AppHub cached builds are available, the SDK will default to using the build that was submitted to the App Store.

---

<h3 short-title='Network Usage'>Network Usage</h3>

The AppHub SDK polls for new builds of your app and downloads new builds in a background thread.

By default, the AppHub SDK will only poll for new builds when the device is connected to WiFi.

You can permit the SDK to download new builds on a cellular connection (WWAN) like so:

    [AppHub buildManager].cellularDownloadsEnabled = YES;

---

<h3 short-title='Listening for New Builds'>Listening for New Builds</h3>

If you want to perform an action when a new build becomes available to your application, such as displaying an alert to the user or force refreshing the app, you can listen for new build events.

From JavaScript you can register a listener for this event like so:

    var { NativeAppEventEmitter, AlertIOS } = React;
    var subscription = NativeAppEventEmitter.addListener(
      'AppHub.newBuild',
      (build) => {
        // Show a modal, alert the user, etc...
        AlertIOS.alert('New version available!', build.buildDescription);
      }
    );

From Objective-C you can observe notifications with the name `AHBuildManagerDidMakeBuildAvailableNotification`:

    [[NSNotificationCenter defaultCenter]
      addObserverForName:AHBuildManagerDidMakeBuildAvailableNotification
                  object:nil
                   queue:nil
              usingBlock:^(NSNotification *notification) {
          AHBuild *build = notification.userInfo[AHBuildManagerBuildKey];
          NSLog(@"New build available! %@", build.buildDescription);
      }];
---

<h3 short-title='Debug Builds'>Debug Builds</h3>

Many developers use AppHub with testing services like TestFlight and HockeyApp as it is desirable to push AppHub updates to your beta users before pushing them to production.

To enable "debug" builds, enable this property in your Objective-C code and distribute
to beta users:

    [AppHub buildManager].debugBuildsEnabled = YES;

When deploying builds from the AppHub dashboard, configure your build to deploy to the "debug" target.

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

<h3 short-title='Polling for New Builds'>Polling for New Builds (Advanced)</h3>

The AppHub SDK will poll our servers for new builds of your App.

If you wish to manually control the frequency and timing of the polling, you can disable automatic polling:

    [AppHub buildManager].automaticPollingEnabled = NO;

To poll for new builds, call this method:

    [[AppHub buildManager] fetchBuildWithCompletionHandler:nil];

This method can also take a completion block as an argument:

    [[AppHub buildManager] fetchBuildWithCompletionHandler:
        ^(AHBuild *result, NSError *error) {
      // If the `result` AHBuild is not nil, then it is guaranteed
      // to be the most up-to-date build of the app.
    }];

Some developers choose to use this method at App startup to ensure that all devices have the most
up-to-date build.
