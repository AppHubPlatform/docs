
<h2>REST API</h2>

We provide an endpoint for uploading builds to the AppHub dashboard.

It is also possible to automatically upload builds from continuous integration services. We provide instructions here for two popular services: [Travis CI](https://travis-ci.org/) and [CircleCI](https://circleci.com/).

---

<h3 short-title='PUT Endpoint'>PUT Endpoint</h3>

You can use the AppHub API to upload IPA files. Here is an example which uses cURL:

    curl -X PUT \
         -H "X-AppHub-Application-ID: <App ID>" \
         -H "X-AppHub-Application-Secret: <App Secret>" \
         -L https://api.apphub.io/v1/upload \
         --upload-file <IPA Location>

Replace `<App ID>`, `<App Secret>`, and `<IPA Location>` with the appropriate values.

---

<h3 short-title='Uploading from Travis'>Uploading from Travis</h3>

Section under construction.

---

<h3 short-title='Uploading from CircleCI'>Uploading from CircleCI</h3>

Section under construction.