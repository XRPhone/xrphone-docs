## Configuring Auth0

**Step 1- Creating Auth0 Application**

- Create a Free plan on https://auth0.com
- Once your logged-in to the auth0 dashboard go to the **Applications > Application** section and tap the button **Create Application** button.

<img src="https://files.readme.io/d610ee0-Screen_Shot_2022-07-22_at_3.18.06_PM.png" class="border" />
<div class="caption">Tap on the **Applications** section on the left-side of the Auth0 navigation then click the <b>Create Application</b> button.</div>

- Enter the name of your app
- Select the option **Regular Web Applications** 

<img src="https://files.readme.io/825ee0e-Screen_Shot_2022-07-22_at_3.29.57_PM.png" class="border" />
<div class="caption">Enter the <b>Name</b> of your app and choose an application type of <b>Regular Web Applications</b>.</div>

- Once your app is created tap on the Settings tab

<img src="https://files.readme.io/c134c13-Screen_Shot_2022-07-22_at_3.48.39_PM.png" class="border" />

- The only required setting you must configure is the setting: **Allowed Callback URLs**.

**Allowed Callback URLs** should be set to the value `https://api.xrphone.app/custom-apps/oauth`

- In addition we recommend configuring the **Application Logo** setting with your application logo.

>[!WARNING]
>Please take note of your Auth0 application **Domain**, **Client ID**, and **Client Secret**. You will need them in the next steps.

**Step 2- Creating Auth0 API**
- Tap on the left-side Auth0 navigation section **Applications > APIs**
- Tap on the button **Create API**

<img src="https://files.readme.io/33c0df0-Screen_Shot_2022-07-22_at_4.04.02_PM.png" class="border" />

- Enter a **Name** for the Auth0 API. For example `My App`. 
- Enter an **Identifier**: For example `my-api` 

You can leave the **Signing Algorithm** with default of `RS256` 

>[!WARNING]
>Please take note of the **Identifier**. You will need this in the upcoming steps.

- Once the API has been created scroll down to **Access Settings** to enable the **Allow Offline Access** setting and then click **Save** button.

<img src="https://files.readme.io/c26faf7-Screen_Shot_2022-07-22_at_4.13.53_PM.png" class="border" />

- Tap the **Create** button.

## Configuring XRPhone

**Step 1- Creating XRPhone Custom App**

- Log In / Sign Up account on the [XRPhone Developer Portal](https://developer.xrphone.app)

<img src="https://files.readme.io/3fc6c4b-Screen_Shot_2022-07-22_at_4.21.05_PM.png" class="border" />
<div class="caption">If you have not yet created account tap the <b>Sign Up</b> tab. If you already have an account use the <b>Log In</b> tab.</div>

- On the left-side navigation click on **Apps* 

- Click **Create app**

<img src="https://files.readme.io/4f36142-Screen_Shot_2022-07-22_at_1.25.34_PM.png" class="border" />

- Under the **General** section you will need to fill in all of the fields (**Name, Description, Homepage, Support Url, Support Email, Icon Url** with your app information. 

<img src="https://files.readme.io/a7b149b-Screen_Shot_2022-07-22_at_1.31.43_PM.png" class="border" />
<div class="caption">Fill in all of the app general information.</div>

 - Next, we will need to fill in the **Connection** settings. These are the settings that are used to authenticate XRPhone Merchants with your application. This is what enables XRPhone to perform invoice lookup and invoice payments with your external application.

<img src="https://files.readme.io/6421737-Screen_Shot_2022-07-22_at_1.43.51_PM.png" class="border" />

Let's now fill in the connection fields using some of the information we obtained from earlier when we created the Auth0 application.

>[!WARNING]
><b>Replace the values in brackets</b><br>
All of the values below with bracket need to be replaced with the literal value. If for example the value of your Auth0 app domain was `foo.us.auth0.com` then you would replace `<YOUR_AUTH0_APP_DOMAIN>` with `foo.us.auth0.com`.

**Authorization Url**
`https://<YOUR_AUTH0_APP_DOMAIN>/authorize?client_id=<YOUR_AUTH0_APP_CLIENT_ID>&response_type=code&redirect_uri=https://api.xrphone.app/custom-apps/oauth&scope=offline_access&audience=<YOUR_AUTH0_APP_IDENTIFIER>`

**Token Url**
`https://<YOUR_AUTH0_APP_DOMAIN>/oauth/token`

>[!NOTE]
><b>Where do I find my apps Webhook Url?</b><br>
The **Webhook Url** should point to your remote server which hosts the custom app API. The XRPhone platform will send webhook POST requests to your app API server. **For example:** `https://api.my-app.com/xrphone/webhook-callback`. In the example above the developer configured a host called `api.my-app.com` with a `POST` endpoint resource located at path `/xrphone/webhook-callback`. You will use any host and any resource path you wish to use. Just make sure you provide that in this field. This is where XRPhone will send the webhook requests like `INVOICE_LOOKUP` and `INVOICE_PAYMENT`.

**Webhook Url**
`<YOUR_WEBHOOK_URL>`

**Client ID**
`<YOUR_AUTH0_APP_CLIENT_ID>`

**Client Secret** 
`<YOUR_AUTH0_APP_CLIENT_SECRET>`

- After we have filled in all of the required fields click the button **Save**

- When the app is created a unique **API Key** and **API Secret** are generated for this specific application. 

<img src="https://files.readme.io/511c773-Screen_Shot_2022-07-22_at_2.01.08_PM.png" class="border" />
<div class="caption">Take note of the <b>API Key</b> and <b>API Secret</b>.</div>

We have now officially completed all of the application configuration. Next we will configure an example application code.

>[!NOTE]
><b>Note about Custom App Example</b><br>
The steps below utilize [Node.js](https://nodejs.org) (server-side JavaScript) with the [Express.js](https://expressjs.com) library. In addition, the example showcases the XRPhone SDK Library for Node.js. It should be noted that you can use any language you like. For developers building with other languages you will need to make sure you formulate the webhook payload responses with the correct object body. As of now the SDK handles this for the developers working with Node.js.

## Configuring App Code

As mentioned in the previous section, we will be configuring the [custom app example](https://github.com/XRPhone/xrphone-custom-app-example-expressjs). 

The example custom app exposes an Express.js API which uses Node.js (server-side JavaScript). 

The Express.js API includes a POST route handler `/webhook/callback` which is what will receive the webhook requests from the XRPhone server when a customer attempts a merchant invoice lookup/payment. 

The route is configured with Auth0 middleware `requiresAuth` which will verify that the XRPhone server merchant authorization credentials are valid and eligible to call the app. 

1. Follow the steps [here](/v1/developer-portal/custom-app-example.md) to clone the example app to your local system and install all package dependencies. 

2. Once this is complete, copy the `.env.example` to `.env`. You can do this by running 

```shell
cp .env.example .env
```

3. Now we need to open the `.env` file to edit the variables to use the correct values for our app configuration.

>[!WARNING]
><b>Example of `.env`</b><br>
Below is an example of what your `.env` file might look like: The values below are all fake.

```shell
XRPHONE_API_KEY=zASluVMaFsAOUNElALVw5qdyXELgB1c9
XRPHONE_API_SECRET=BnJdnQrevvN-g1MuumTg0DBmI36e_RM6dspARdj44nKaJDk1dmsT_b2T5wZ2jN-q
AUTH0_JWKS_URI=https://foo.us.auth0.com/.well-known/jwks.json
AUTH0_AUDIENCE=my-api
AUTH0_ISSUER=https://foo.us.auth0.com/
```

4. This should be all that is required to begin using the sample app. It should be noted that the sample app provides an in-memory MongoDB. This provides temporary non-persistent sample accounting invoice data for testing with XRPhone. Each time you restart the example app the invoice data is reset.

You can view the initial starter data within the custom app location `xrphone-custom-app-example/db/mocks/accounting.mock.ts`

5. When you have finished configuring the `.env` you can run the build

```shell
npm run build
```

> This will run the TypeScript compiler and output the JavaScript build to the `/dist` folder.

6. Now that we have the actual build we can run the server 

```shell
npm run start
```

If everything went as planned, we should have the custom app local server running on default port 3000. In order to make the XRPhone server have the ability to communicate with your local custom app we will want to temporarily run a service like [`ngrok`](https://ngrok.com/). 

The `ngrok` service provides a free reverse-proxy tunnel which gives you a public web address that will automatically route to our locally running custom app. This works great for testing since we don't need to perform an actual deployment on a public server.

```shell
npm install -g ngrok
```

7. Now we want to start ngrok to create a temporary http tunnel for testing with XRPhone.

```shell
ngrok http 3000
```

- You should see your apps public web address that was generated, copy the address to your clipboard.

- Go back into the XRPhone Developer Portal and open the app connection settings and update the **Webhook Url** by pasting the address you just copied and then appending `/webhook/callback`

For example:
`https://c6e8-2600-1700-a761-b920-30ad-aa68-5322-d39c.ngrok.io/webhook/callback`