# deleg

This function of Mimikatz checks for the following types of [Kerberos delegations](https://www.thehacker.recipes/ad-ds/movement/kerberos/delegations)

* Unconstrained Delegation \(`TRUSTED_FOR_DELEGATION`\)
* Constrained Delegation \(`TRUSTED_TO_AUTH_FOR_DELEGATION`, set with the `msDS-Allowed-To-Delegate-To`attribute\)
* Resource Based Constrained Delegation \(set with the `msDS-Allowed-To-Act-On-Behalf-Of-Another-Identity` attribute\)

It has the following command line arguments:

* `/dns`: the active directory domain to query
* `/server`: The domain controller to query. If not specified it will query the DC of the current domain

```text
mimikatz # net::deleg

CN=Win2019,OU=Servers,DC=hacklab,DC=local
  objectGUID: {06a4a894-6e0b-41be-952e-f3c3108a1928}
  userAccountControl: 0x00091000 - WORKSTATION_TRUST_ACCOUNT ; DONT_EXPIRE_PASSWD ; TRUSTED_FOR_DELEGATION ;
  objectSid: S-1-5-21-1874506631-3219952063-538504511-1128
  sAMAccountName: Win2019$
  servicePrincipalName:
    TERMSRV/Win2019
    TERMSRV/Win2019.hacklab.local
    WSMAN/Win2019
    WSMAN/Win2019.hacklab.local
    RestrictedKrbHost/Win2019
    HOST/Win2019
    RestrictedKrbHost/Win2019.hacklab.local
    HOST/Win2019.hacklab.local
```

