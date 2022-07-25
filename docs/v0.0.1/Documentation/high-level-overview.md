**XRPhone consists of the following core components:**
  * Web Client
  * Xumm Wallet xApp Mobile Client
  * Developer Portal Web Client
  * SDK Library (Node.js)
  * Server API

Each of these components will be further expanded on in the different sections of our docs.

Below is a high level diagram depicting current XRPhone system architecture.

<center>
  <img src="https://files.readme.io/cba3233-XRPhone-diagram-high-level-1.jpg"/>
  <div class="caption">Diagram showing high level overview of the current XRPhone platform.</div>
</center>

Let's jump into this diagram to better understand how XRPhone routes inbound requests.

In this example diagram we have the **Inbound Caller with Xumm Wallet**.  

When the caller dials the XRPhone toll-free number the call is routed to [Twilio](https://twilio.com). Twilio bridges the inbound call into an interactive voice response (IVR) system which interacts directly with the **XRPhone Server API**. 

The active inbound call contains metadata such as the phone number of the caller. **XRPhone Server API** takes this phone number and checks with the **Supabase Postgres DB** to confirm that the caller has an active XRPhone customer account. We need to make sure the inbound caller has already setup their phone number with XRPhone because this is how the XRPhone system is able to to send a push notification to the active callers Xumm wallet containing the correct merchant invoice payment request details.

If the caller is not found in the database they will be instructed to create an XRPhone account to link with their mobile phone number. XRPhone accounts can be created either thru the **XRPhone Web Client** or via the **XRPhone Xumm xApp Mobile Client**.
[block:callout]
{
  "type": "info",
  "body": "Currently XRPhone Merchant accounts can only be created thru the **XRPhone Web Client**. Regular customer accounts can use either interface to establish an account.",
  "title": "Note regarding XRPhone Merchant Account Creation"
}
[/block]
Assuming the active caller was found in the **Supabase Postgres DB**, the voice response system asks the caller to enter the XRPhone Merchant phone number for the invoice they will be paying with XRP.

---

XRPhone Merchants are businesses who have linked both an XRP account and supported XRPhone invoice accounting platform integration. Merchants can use either a self-custody based XRPL account (e.g: Xumm Wallet) or centralized exchange (CEX) based account with destination tag (e.g: Uphold, KuCoin) to receive XRP . 

---

Assuming the requested XRPhone Merchant phone number is found, the voice response system will ask the caller to enter the invoice number they are applying payment.

The **XRPhone Server API** will perform an invoice lookup to the merchants connected invoice accounting platform integration. 

For example: If the merchant was using Quickbooks Online, then the **XRPhone Server API** requests from **Quickbooks Online Integration** the current amount due on the invoice and returns this information back to the **XRPhone Server API** which in return responds via the voice response system to the caller with the current invoice balance.

The caller is then asked to enter into the phone keypad the amount they wish to pay based on the invoices fiat currency type (e.g: USD).

After the invoice amount is provided the **XRPhone Server API** communicates with **XRPL API** to obtain the current price of XRP. This is used to convert the requested invoice denominated fiat currency amount into the equal XRP value. 

When the current XRP price is obtained the **XRPhone Server API** communicates with the **Xumm API** to initiate a payment transaction. This is accomplished by sending "on-the-fly" an instant push notification to the callers mobile device while on the active phone call. The push notification contains the transaction details needed to collect the correct XRP payment amount from the caller. 

Once the caller swipes the transaction within Xumm wallet, the transaction is approved and the XRP Ledger settles the transaction between the caller and merchant, usually within seconds. When the payment is completed, the **Xumm API** sends a webhook callback to the **XRPhone Server API** indicating the transaction was successful. 

The **XRPhone Server API** takes the successful payment notification sent by Xumm and then updates the invoice found within the merchants connected invoice accounting integration (e.g: **Quickbooks Online Integration**).

This results in the merchant receiving XRP for the invoice and also maintaining up-to-date account balance within their businesses invoice accounting software. In addition it enabled the customer to use XRP to make payment on the open invoice.