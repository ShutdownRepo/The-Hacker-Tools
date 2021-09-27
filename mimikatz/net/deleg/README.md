# deleg

This function of Mimikatz checks for the following types of [Kerberos delegations](https://www.thehacker.recipes/ad-ds/movement/kerberos/delegations)

* Unconstrained Delegation \(`TRUSTED_FOR_DELEGATION`\)
* Constrained Delegation \(`TRUSTED_TO_AUTH_FOR_DELEGATION`, set with the `msDS-Allowed-To-Delegate-To attribute`\)
* Resource Based Constrained Delegation \(set with the `msDS-Allowed-To-Act-On-Behalf-Of-Another-Identity` attribute\)

```text
mimikatz # net::deleg

CN=DCORP-APPSRV,OU=Servers,DC=dollarcorp,DC=moneycorp,DC=local
  objectGUID: {06a4a894-6e0b-41be-952e-f3c3108a1928}
  userAccountControl: 0x00091000 - WORKSTATION_TRUST_ACCOUNT ; DONT_EXPIRE_PASSWD ; TRUSTED_FOR_DELEGATION ;
  objectSid: S-1-5-21-1874506631-3219952063-538504511-1128
  sAMAccountName: DCORP-APPSRV$
  servicePrincipalName:
    TERMSRV/DCORP-APPSRV
    TERMSRV/dcorp-appsrv.dollarcorp.moneycorp.local
    WSMAN/dcorp-appsrv
    WSMAN/dcorp-appsrv.dollarcorp.moneycorp.local
    RestrictedKrbHost/DCORP-APPSRV
    HOST/DCORP-APPSRV
    RestrictedKrbHost/dcorp-appsrv.dollarcorp.moneycorp.local
    HOST/dcorp-appsrv.dollarcorp.moneycorp.local
```

