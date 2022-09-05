# cloudapkd 🛠️

`dpapi::cloudapkd` allows to decrypt via DPAPI the ProofOfPossesionKey (extracted from a Primary Refresh Token, a.k.a. PRT, e.g. [cloudap.md](../sekurlsa/cloudap.md "mention")) and thus recover the Clear key and the Derived Key.

* `/prt`: Primary Refresh Token, used for JWT token generation (can be found with `sekurlsa::cloudap`)
* `/iat`: Issued At, used for JWT token generation (Default: -112)
* `/pop`: Proof-of-Possession (Unknown usage, Work In Progress)
* `/label`: Object label, can be retrive from `keyvalue` with `unprotect`
* `/context`: Used for JWT token generation (can be found with unprotect)
* `/keyname`: Is necessary for opaque keys (when a TPM is used for example) during `unprotect` operation
* `/keyvalue`: Part of ProofOfPossesionKey, can be found with `sekurlsa::cloudap`. Unprotect this data to retrieve `context`, `label`, `clearkey` and `derivedkey`
* `/derivedkey`: used for JWT token generation (can be found with unprotect)
* `/unprotect`: Decrypt the secret from DPAPI (`masterkey` is optionnal, but `token::elevate` is required)
* `/masterkey`: master DPAPI key use to unprotect the secret (can be retrieved from `sekurlsa::dpapi`). This field is **not mandatory**, if absent the key will be found automatically

### References

{% embed url="https://o365blog.com/post/prt/" %}

{% embed url="https://stealthbits.com/blog/lateral-movement-to-the-cloud-pass-the-prt/" %}

{% embed url="https://dirkjanm.io/digging-further-into-the-primary-refresh-token" %}

{% embed url="https://derkvanderwoude.medium.com/pass-the-prt-attack-and-detection-by-microsoft-defender-for-afd7dbe83c94" %}

{% embed url="https://twitter.com/gentilkiwi/status/1290930755380576256" %}
