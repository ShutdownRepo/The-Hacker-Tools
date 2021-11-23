# ask

`kerberos::ask` can be used to obtain Service Tickets. The Windows native command is [`klist get`](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/klist). It has the following command line arguments:

* `/tkt`: save the ST (Service Ticket) to a `.tkt` file
* `/export` : export the TGS to a `.kirbi` file
* `/rc4` : use an RC4 key
* `/des` : use a DES key
* `/aes256` : use an AES256 key (it is the default key)
* `/aes128` : use an AES128 key
* `/target` : The target SPN/FQDN
* `/nocache`: tells Mimikatz not to cache the ticket in the current session

```
mimikatz # kerberos::ask 0-40e10000-m3g9tr0n@krbtgt~HACKLAB.LOCAL-HACKLAB.LOCAL.kirbi /target:CIFS/dc.hacklab.local
Asking for: CIFS/dc.hacklab.local
   * Ticket Encryption Type & kvno not representative at screen

           Start/End/MaxRenew: 18/11/2021 01:47:30 ; 18/11/2021 11:47:30 ; 25/11/2021 01:47:30
           Service Name (02) : CIFS ; dc.hacklab.local ; @ HACKLAB.LOCAL
           Target Name  (02) : CIFS ; dc.hacklab.local ; @ HACKLAB.LOCAL
           Client Name  (01) : m3g9tr0n ; @ HACKLAB.LOCAL
           Flags 40a50000    : name_canonicalize ; ok_as_delegate ; pre_authent ; renewable ; forwardable ;
           Session Key       : 0x00000012 - aes256_hmac
             9905bb3a8b7b45f9c841983c7a7e3e0c0cc197e879fd6933a70f29227c6c8e21
           Ticket            : 0x00000012 - aes256_hmac       ; kvno = 0        [...]
```

Check if the ST was injected in the current session:

```
mimikatz # kerberos::list

[00000000] - 0x00000012 - aes256_hmac
   Start/End/MaxRenew: 18/11/2021 01:47:30 ; 18/11/2021 11:47:30 ; 25/11/2021 01:47:30
   Server Name       : krbtgt/HACKLAB.LOCAL @ HACKLAB.LOCAL
   Client Name       : m3g9tr0n @ HACKLAB.LOCAL
   Flags 40e10000    : name_canonicalize ; pre_authent ; initial ; renewable ; forwardable ;

[00000001] - 0x00000012 - aes256_hmac
   Start/End/MaxRenew: 18/11/2021 01:47:30 ; 18/11/2021 11:47:30 ; 25/11/2021 01:47:30
   Server Name       : CIFS/dc.hacklab.local @ HACKLAB.LOCAL
   Client Name       : m3g9tr0n @ HACKLAB.LOCAL
   Flags 40a50000    : name_canonicalize ; ok_as_delegate ; pre_authent ; renewable ; forwardable ;
```

Request a ST for `HTTP/dc.hacklab.local` with an RC4 key:

```
mimikatz # kerberos::ask /rc4 0-40e10000-m3g9tr0n@krbtgt~HACKLAB.LOCAL-HACKLAB.LOCAL.kirbi /target:HTTP/dc.hacklab.local
Asking for: HTTP/dc.hacklab.local
   * Ticket Encryption Type & kvno not representative at screen

           Start/End/MaxRenew: 18/11/2021 02:08:15 ; 18/11/2021 11:47:30 ; 25/11/2021 01:47:30
           Service Name (02) : HTTP ; dc.hacklab.local ; @ HACKLAB.LOCAL
           Target Name  (02) : HTTP ; dc.hacklab.local ; @ HACKLAB.LOCAL
           Client Name  (01) : m3g9tr0n ; @ HACKLAB.LOCAL
           Flags 40a50000    : name_canonicalize ; ok_as_delegate ; pre_authent ; renewable ; forwardable ;
           Session Key       : 0x00000017 - rc4_hmac_nt
             31186422cb60b903003c8aa0bc1cb384
           Ticket            : 0x00000017 - rc4_hmac_nt       ; kvno = 0        [...]
```
