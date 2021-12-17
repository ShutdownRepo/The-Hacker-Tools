# capi

`crypto::capi` patches CryptoAPI layer for easy export (Experimental :warning:).&#x20;

This patch modifies a `CryptoAPI` function, in the `mimikatz` process, in order to make unexportable keys, exportable (no specific right other than access to the private key is needed). It can be used with [`crypto::certificates`](certificates.md) and [`crypto::keys`](keys.md). This is only useful when the keys provider is one of:

* `Microsoft Base Cryptographic Provider v1.0`
* `Microsoft Enhanced Cryptographic Provider v1.0`
* `Microsoft Enhanced RSA and AES Cryptographic Provider`
* `Microsoft RSA SChannel Cryptographic Provider`
* `Microsoft Strong Cryptographic Provider`

```
mimikatz # crypto::capi
Local CryptoAPI patched
```
