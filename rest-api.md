
<h2>REST API</h2>

We provide an endpoint for uploading builds to the AppHub dashboard.

It is also possible to automatically upload builds from continuous integration services. We provide instructions here for two popular services: [Travis CI](https://travis-ci.org/) and [CircleCI](https://circleci.com/).

---

<h3 short-title='Uploading IPAs'>Uploading IPAs</h3>

You can use the AppHub API to upload IPA files. Here is an example which uses cURL:

    curl -X PUT \
         -H "X-AppHub-Application-ID: <App ID>" \
         -H "X-AppHub-Application-Secret: <App Secret>" \
         -L https://api.apphub.io/v1/upload \
         --upload-file <IPA Location>

Replace `<App ID>`, `<App Secret>`, and `<IPA Location>` with the appropriate values.

Optionally, you can specify additional build metadata with the `X-AppHub-Build-Metadata` header as a JSON object with these keys:

- `target` (String, optional): One of [`all`, `debug`, `none`] which specifies the target audience of the build.
- `description` (String, optional): Description of the build.
- `app_versions` (Array of Strings, optional): Compatible app versions of the build.

Example:

    curl -X PUT \
         -H "X-AppHub-Application-ID: <App ID>" \
         -H "X-AppHub-Application-Secret: <App Secret>" \
         -H 'X-AppHub-Build-Metadata: {
              "target": "all",
              "description": "Awesome build!",
              "app_versions": ["1.0", "1.1"]
            }' \
         -L https://api.apphub.io/v1/upload \
         --upload-file <IPA Location>

---

<h3 short-title='Uploading from Travis'>Uploading from Travis</h3>

Section under construction.

---

<h3 short-title='Uploading from CircleCI'>Uploading from CircleCI</h3>

Section under construction.