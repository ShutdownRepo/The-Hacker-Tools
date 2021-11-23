# list

`kerberos::list` has a similar functionality to [`klist`](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/klist) command without requiring elevated privileges. Unlike [`sekurlsa::tickets`](../sekurlsa/tickets.md), this module does not interact with LSASS. It has the following command line argument:

* `/export`: export the tickets

```
mimikatz # kerberos::list

[00000000] - 0x00000012 - aes256_hmac
   Start/End/MaxRenew: 15/11/2021 18:27:08 ; 16/11/2021 04:27:08 ; 17/11/2021 11:41:46
   Server Name       : krbtgt/HACKLAB.LOCAL @ HACKLAB.LOCAL
   Client Name       : m3g9tr0n @ HACKLAB.LOCAL
   Flags 40e10000    : name_canonicalize ; pre_authent ; initial ; renewable ; forwardable ;

[00000001] - 0x00000012 - aes256_hmac
   Start/End/MaxRenew: 15/11/2021 18:47:48 ; 16/11/2021 04:27:08 ; 17/11/2021 11:41:46
   Server Name       : LDAP/DC.hacklab.local/hacklab.local @ HACKLAB.LOCAL
   Client Name       : m3g9tr0n @ HACKLAB.LOCAL
   Flags 40a50000    : name_canonicalize ; ok_as_delegate ; pre_authent ; renewable ; forwardable ;
```
