
<h2>Downloads & Changelogs</h2>

This section contains a list of the lastest versions of each SDKs, as well as a changelog for each
SDK.

---

<h3 short-title='Latest SDKs'>Latest SDKs</h3>

- iOS: [SDK](https://www.dropbox.com/s/o0lyimm7qg5l7ay/AppHub.zip?dl=1) (v0.0.8)

<h3 short-title='iOS Changelog'>iOS Changelog</h3>

- v0.0.8 - August 28, 2015
  - Changed the default fetching mechanism to only download new builds on a WiFi connection. This
    behavior can be configured via the `cellularDownloadsEnabled` property on `AHBuildManager`. See
    [the docs](/docs/getting-started#docs-network-usage) for more information on this feature.
  - Changed `fetchBuildWithCompletionHandler` to only return a non-nil `AHBuild` instance if the SDK
    has fetched the most up-to-date build. See [the docs](/docs/getting-started#docs-polling-for-new-builds)
    for more information.

- v0.0.7 - August 24, 2015
  - Fixed a bug which caused iOS 7 clients to update to newer JavaScript bundles without updated images.