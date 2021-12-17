# certtohw

`crypto::certtohw` tries to export a software CA to a crypto (virtual) hardware. It has the following command line arguments:

* `/csp`: the crypto certificate provider
* `/name`: the name of the certificate
* `/store`: the store that must be used to list/export certificates (default: `My`) - full list with [`crypto::stores`](stores.md).
