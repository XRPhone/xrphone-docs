>[!WARNING]
>This feature is not yet released for public usage.

1. Once you are logged into the developer portal you will want to access the Apps section found on the left side navigation bar. Then tap the the **Create App**.  Below we have added a red arrow to illustrate.

<img src="https://files.readme.io/c7f41e6-Screen_Shot_2022-07-22_at_1.25.34_PM.png" class="border" />
<div class="caption">From the Apps section of the Developer Portal tap the Create App button to begin.</div>

2. Now you will need to provide all of the details regarding your app. The app creation page consists of General and Connection settings.

## General Settings 

<img src="https://files.readme.io/d9c619e-Screen_Shot_2022-07-22_at_1.31.43_PM.png" class="border" />
<div class="caption">The apps General settings.</div>

Let's review the different parts of the general settings:

**Listed / Sandboxed / Debug Merchant #** 
When you initially create an XRPhone app, the app is defaulted to **Sandboxed**. 

>[!NOTE]
><b>Sandboxed Apps</b><br>
Sandboxed means that the app will not appear on the XRPhone Merchant Integration Marketplace. The marketplace is where merchants connect  to their supported invoice accounting platform. For example the core XRPhone supported integrations would be (e.g: Quickbooks Online, Xero, etc).

To make a developer app appear for all XRPhone Merchants the app needs to be toggled from **Sandboxed** to **Listed**. When an app has been tested by the developer and is ready to be listed, they would contact XRPhone who will perform the toggling.

While the app is in the development stages and sandboxed in-order to interact with the app you will want to enter the **Debug Merchant #**. 

>[!NOTE]
><b>Debug Merchant #</b><br>
**Debug Merchant #** is the phone number linked to a XRPhone Merchant account. When this number is provided the XRPhone Merchant will be able to use this app by connecting it to their account. The app will be marked as Sandboxed. This setting enables the app developer to enable a XRPhone Merchant to test their app integration.

**Name** 
This is the name of the app.

**Description**
This is a brief description of the app.

**Homepage** 
The homepage for the app.

**Support Url**
The support url for the app.

**Support Email**
The support email for the app.

**Icon Preview**
This will automatically update when an **Icon Url** is provided.

**Icon Url**
The app icon image. When this is added the **Icon Preview** will show the image. 

## Connection Settings

<img src="https://files.readme.io/dca6cd3-Screen_Shot_2022-07-22_at_1.43.51_PM.png" class="border" />
<div class="caption">The connection settings that XRPhone will use to establish a connection with the external application.</div>

To enable XRPhone to communicate with the external application, XRPhone requires that the app support [oAuth Authorization Code Flow](https://auth0.com/docs/get-started/authentication-and-authorization-flow/authorization-code-flow).

To make it simple for XRPhone developers to provide oAuth Authorization Code Flow we recommend using [Auth0](https://auth0.com). If you have not yet configured your app for Auth0 [please first follow these steps](https://foo.com).

Once you have the required connection settings we can fill them in:

**Authorization Url**
This is your apps oAuth authorization url used by XRPhone to obtain an authorization code from your apps oAuth server. 

**Token Url**
This is your apps oAuth token url used by XRPhone to obtain an access/refresh token for the merchant connecting XRPhone to your app.

**Webhook Url**
This is the apps webhook url used by XRPhone to send invoice lookup and invoice payment requests to your application. XRPhone makes these external requests to your application with the obtained access token claimed for the XRPhone Merchant using your integrated app.

**Client ID**
This is the client id associated with your oAuth application.

**Client Secret**
This is the client secret associated with your oAuth application.

3. After we have entered all of the fields for the app click the **Save** button. 

<img src="https://files.readme.io/5e714d2-Screen_Shot_2022-07-22_at_2.01.08_PM.png" class="border" />
<div class="caption">Once your app has been created you will see a new section on the page called Credentials.</div>

Each app you create will contain a special **Credentials**.

**API Key**
This key will always stay the same. You can tap the Copy button to easy add to your clipboard.

**API Secret** 
This is a secret that you should not ever let anyone see. Keep this secure. If for some reason the secret is compromised you can click **Regenerate Secret**. Remember, if you regenerate the secret you will need to update your application to use this new secret since the old one is no longer valid. 

>[!NOTE]
><b>API Key & API Secret</b><br>
These credentials are used for example in the [XRPhone SDK Library (Node.js) ](/v0.0.1/SDK%20Libraries/xrphone-sdk-nodejs). They are needed when the application is responding to a webhook request.
