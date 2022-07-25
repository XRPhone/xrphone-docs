>[!NOTE]
><b>How are app logs created?</b><br>
When XRPhone communicates with a [custom app](/v1/developer-portal/creating-custom-app.md), a [webhook](https://en.wikipedia.org/wiki/Webhook) is triggered that calls the external application and will await a response.

For example, let's say we have a merchant who connected a custom app called "Super Cool Accounting App". This is an app created by an external developer who an XRPhone merchant needs to interface with. 

When the merchants customer calls into the XRPhone system, they enter into the mobile phone keypad the invoice number e.g: *1002*, the XRPhone system will send a webhook call for an `INVOICE_LOOKUP` to the "Super Cool Accounting App" webhook url. 

Later when the customer makes payment with XRP and the transaction is settled on the XRPL, XRPhone will send another webhook with topic `INVOICE_PAYMENT` to the "Super Cool Accounting App".

Developers can view all of the attempted webhook requests to their apps using the Developer Portal Logs screen. This can be especially helpful when developing / debugging during the app creation process.

The logs are composed of the following columns:

**Webhook Topic**
The app topic that the webhook request belongs. XRPhone sends in the request headers `X-XRPhone-Topic`. These topics relate to the type of data being requested from the custom app.

**Payload UUID**
Unique identifier that is associated to the specific log entry (webhook request) made to the custom app.

**Created At**
Provides date/time when the log entry was generated.

Below is an example sceenshot:

<img src="https://files.readme.io/8591d1c-Screen_Shot_2022-07-22_at_2.50.36_PM.png" class="border" />
<div class="caption">Developer reviewing log entry for an `INVOICE_LOOKUP` made by XRPhone to their app.</div>
