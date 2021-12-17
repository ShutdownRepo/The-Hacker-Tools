# 🛠️ scauth

{% hint style="danger" %}
Work in progress
{% endhint %}

`crypto::scauth` it creates a authentication certificate (smartcard like) from a CA. It has the following command line arguments:

* `/hw:` at the time of writing, 17th December 2021, we don't know what this option is used for
* `/csp:` the crypto certificate provider
* `/pin:` the smartcard PIN
* `/nostore:` do not interact with the store
* `/caname`: the subject name of the certificate authority (needed to sign the certificate)
* `/castore`: the system store that contains the certificate authority (default: `CERT_SYSTEM_STORE_LOCAL_MACHINE`)
* `/upn`: the User Principal Name (UPN) targeted (eg: `user@lab.local`)
* `/pfx`: the filename for saving the final certificate (default: no file, stored in `CERT_SYSTEM_STORE_CURRENT_USER`)

```
mimikatz # crypto::scauth /caname:KiwiAC /upn:user@lab.local /pfx:user.pfx
CA store       : LOCAL_MACHINE
CA name        : KiwiAC
CA validity    : 22/08/2016 22:00:36 -> 22/08/2021 22:10:35
Certificate UPN: user@lab.local
Key container  : {a1bd29ec-4203-4aac-8159-40f28f96335b}
Key provider   : Microsoft Enhanced Cryptographic Provider v1.0
Private Export : user.pfx - OK
```
