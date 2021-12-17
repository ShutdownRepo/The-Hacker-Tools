# keys

`crypto::keys` lists or exports key containers. It has the following command line arguments:

* `/provider`: the legacy `CryptoAPI` provider (default: `MS_ENHANCED_PROV`)
* `/providertype`: the legacy `CryptoAPI` provider type (default: `PROV_RSA_FULL`)
* `/cngprovider`: the `CNG` provider (default: `Microsoft Software Key Storage Provider`)
* `/export`: export all keys to `PVK` files
* `/silent`: if user interaction is required, then abort

{% hint style="info" %}
If needed, you can convert `PVK` files with: `openssl rsa -inform pvk -in key.pvk -outform pem -out key.pem`
{% endhint %}

```
mimikatz # crypto::keys /export
 * Store         : 'user'
 * Provider      : 'MS_ENHANCED_PROV' ('Microsoft Enhanced Cryptographic Provider v1.0')
 * Provider type : 'PROV_RSA_FULL' (1)
 * CNG Provider  : 'Microsoft Software Key Storage Provider'

CryptoAPI keys :

CNG keys :
    0. Microsoft Connected Devices Platform device certificate
        |Provider name : Microsoft Software Key Storage Provider
        |Implementation: NCRYPT_IMPL_SOFTWARE_FLAG ;
        Key Container  : Microsoft Connected Devices Platform device certificate
        Unique name    : de7cf8a7901d2ad13e5c67c29e5d1662_e4aad2d1-5ec0-4ea4-b259-65eda5bc47a8
        Algorithm      : ECDSA_P256
        Key size       : 256 (0x00000100)
        Export policy  : 00000003 ( NCRYPT_ALLOW_EXPORT_FLAG ; NCRYPT_ALLOW_PLAINTEXT_EXPORT_FLAG ; )
        Exportable key : YES
        LSA isolation  : NO
        Private export : OK - 'user_cng_0_Microsoft Connected Devices Platform device certificate.dsa.ec.p8k'
```
