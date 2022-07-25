<script>
    setTimeout(() => {
       if(location.pathname === '/') {
            document.querySelector('.sidebar-nav > ul > li:nth-child(2) > p').classList.add('active');
        }        
    }, 250);

</script>
## Welcome to XRPhone Docs!

> [!NOTE]
> XRPhone is not yet released for public usage. Documentation is subject to change. To keep up to date with XRPhone please follow us on Twitter [@XRPhoneOfficial](http://twitter.com/XRPhoneOfficial)

[XRPhone](https://xrphone.app) is an invoice accounting bridge for the [XRP Ledger](https://xrpl.org).

XRPhone enables merchants using invoice accounting platforms like [Quickbooks Online](https://quickbooks.intuit.com/online) to accept the digital asset virtual currency [XRP](https://ripple.com/xrp) as payment method from their customers over the phone.

XRPhone is an interactive voice response (IVR) system behaving as a virtual concierge sending payment requests to customers [Xumm](https://xumm.app) wallets and automatically applying payment to merchants invoices in real-time maintaining synchronized customer account balances.

At the root of XRPhone is our "Invoice Accounting Bridge". Utilizing the phone (interactive voice response) is only one entry method for making payment. XRPhone is [experimenting with different alternate payment entry methods](/v0.0.1/Proof%20of%20Concepts/merchant-chrome-extension.md) that XRPhone Merchants can utilize. For example: customers can generate sharable links and send them via SMS, email, or simple copy-paste. These shareable links will enable customers to make payment directly on the merchant invoice.