# tgt

`kerberos::tgt` retrieves a TGT (Ticket-Granting Ticket) for the current user.

```
mimikatz # kerberos::tgt
Kerberos TGT of current session :
           Start/End/MaxRenew: 17/11/2021 21:48:12 ; 18/11/2021 07:48:12 ; 24/11/2021 12:03:10
           Service Name (02) : krbtgt ; HACKLAB.LOCAL ; @ HACKLAB.LOCAL
           Target Name  (--) : @ HACKLAB.LOCAL
           Client Name  (01) : m3g9tr0n ; @ HACKLAB.LOCAL
           Flags 40e10000    : name_canonicalize ; pre_authent ; initial ; renewable ; forwardable ;
           Session Key       : 0x00000012 - aes256_hmac
             0000000000000000000000000000000000000000000000000000000000000000
           Ticket            : 0x00000012 - aes256_hmac       ; kvno = 0        [...]

        ** Session key is NULL! It means allowtgtsessionkey is not set to 1 **
```
