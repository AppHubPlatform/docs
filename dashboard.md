<h2>Using the Dashboard</h2>

The AppHub dashboard provides a visual interface for uploading, configuring, and deploying builds to your app. To get started, simply sign in with GitHub and create an app.

<img src='/images/dashboard_screenshot.png'>

AppHub “apps” represent the apps that you distribute to your users. In general, developers create one AppHub “app” for their iOS app, however, if you have multiple version of your app (eg. a production version and a testing version), it may make sense to have separate AppHub apps for each.

---

<h3 short-title='Getting Started'>Getting Started</h3>

When you create an app, the quickstart guide provides step-by-step instructions for integrating the AppHub SDK and connecting your first device.

Once you have connected a device, the indicator in step 5 of the quickstart guide will turn green and you can proceed to uploading builds.

---

<h3 short-title='Uploading Builds'>Uploading Builds</h3>

Builds represent versions of your app. When you upload a new build, the default configuration option is “none” which means your build won't be distributed to any users. In order to deploy your build to your users, click “configure” and select a deployment strategy. “All” deployments go to all of your users. If you have multiple builds with the “all” deployment strategy, users will get the newest build you have uploaded.

<img src='/images/build_modal.png'>

“Debug” builds are distributed to devices that have debug mode enabled through the AppHub SDK. Typically, developers enable the debug option on devices used for testing (eg. their team's devices).

---

<h3 short-title='JS/Native Versioning'>JavaScript and Native Versioning</h3>

It is important for AppHub developers to understand the relationship between iOS app versions and build versions. When you make changes to native code, and change the iOS version of your app, you risk making your app incompatible with javascript code made for earlier native versions. When you upload an IPA to AppHub, we determine the native version of your app associated with the javascript you intend to update. By default, AppHub will then only distribute your javascript update to devices running that native version of your app.

<img src='/images/multiple_versions.png'>

If, however, you wish specify additional native versions of your app to which a build can be distributed, you must enable “Advanced Deployment Settings” in your user account settings. You can access this by clicking your name in the upper right corner of the dashboard and clicking “Account”. Once this setting is enabled, click “configure” on the build you wish to deploy, and you will have the option to specify additional native versions for that build.

---

<h3 short-title='Adding Collaborators'>Adding Collaborators</h3>

If you are collaborating on an app with other developers, you can add collaborators to your app from either the home screen, or the app's settings page (by clicking on the gear in the upper right corner of the app preview). Collaborators can upload and deploy new builds, edit project data, and access usage information, but are not able to invite/remove other collaborators, edit billing information or delete projects.

<img src='/images/collaborators.png'>