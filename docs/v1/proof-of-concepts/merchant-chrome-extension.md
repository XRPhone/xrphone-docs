## XRPhone Merchant Chrome Extension for Quickbooks Online

>[!WARNING]
><b>Lab Experiment</b><br>
This is only a proof of concept to further illustrate alternative "non-phone" entry method to make payment on a XRPhone Merchant invoice.

<img src="https://files.readme.io/d460d90-chrome-extension.png" class="border" />

The primary entry point for people to make payment for an invoice is via the interactive voice response (IVR) phone system.

However, the ability to initiate an invoice payment should not be siloed to only the phone system. 
This proof of concept demonstrates the usage of a [Chrome Extension](https://developer.chrome.com/docs/extensions/) which injects into the XRPhone merchants Quickbooks Online web interface. This provides the Quickbooks Online / XRPhone Merchant the ability to easily generate a XRPhone payment link for the selected Quickbooks Online invoice. 

This payment link can then be shared via text-message (SMS), email,  etc. 

When the recipient opens the XRPhone payment link, they are presented with a simple page that shows the current balance due on the invoice. The recipient then enters the fiat amount they wish to apply as payment on the invoice. 

The recipient then can initiate the QR code scan via their Xumm wallet. Once the transaction is settled via Xumm Wallet/XRPL, the merchants connected invoice accounting application is updated to reflect the new invoice balance keeping the accounting fully up-to-date any synced.

The video below demonstrates a quick demo of how this works. In this example we are also experimenting with utilizing the XRPhone ecosystem token XPHO for paying the invoice, you can also use XRP.

>[!NOTE]
>In this video demo we are making payment using the XRPhone ecosystem token [$XPHO](https://xrpl.to/token/xrphone-xpho). This feature works exactly the same when applying payment using $XRP.

<iframe width="500" height="500" src="https://www.youtube.com/embed/6oj2HHxNg0Q" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
