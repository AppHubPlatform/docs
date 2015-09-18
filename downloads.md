
<h2>Downloads & Changelogs</h2>

This section contains the lastest versions of each SDKs, as well as a changelog for each
SDK.

---

<h3 short-title='Latest SDKs'>Latest SDKs</h3>

- iOS: [SDK](https://www.dropbox.com/s/bz0y7z2r3b4fmxz/AppHub.zip?dl=1) (v0.0.8)

<h3 short-title='iOS Changelog'>iOS Changelog</h3>

- v0.0.8 - September 18, 2015
  - Enabled bitcode for building on iOS 9.

- v0.0.7 - September 4, 2015
  - Fixed a bug where a notification would not be emitted when an app returned to the default App Store build.

- v0.0.6 - August 28, 2015
  - Changed the default fetching mechanism to only download new builds on a WiFi connection. This
    behavior can be configured via the `cellularDownloadsEnabled` property on `AHBuildManager`. See
    [the docs](/docs/getting-started#docs-network-usage) for more information on this feature.
  - Changed `fetchBuildWithCompletionHandler` to only return a non-nil `AHBuild` instance if the SDK
    has fetched the most up-to-date build. See [the docs](/docs/getting-started#docs-polling-for-new-builds)
    for more information.

- v0.0.5 - August 24, 2015
  - Fixed a bug which caused iOS 7 clients to update to newer JavaScript bundles without updated images.