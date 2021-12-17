# stores

`crypto::stores` lists cryptographic stores. It has the following command line argument:

* `/systemstore`: the system store that must be used to list stores (default: `CERT_SYSTEM_STORE_CURRENT_USER`)

The `/systemstore` can also be one of the following:

* `CERT_SYSTEM_STORE_CURRENT_USER` or `CURRENT_USER`
* `CERT_SYSTEM_STORE_CURRENT_USER_GROUP_POLICY` or `USER_GROUP_POLICY`
* `CERT_SYSTEM_STORE_LOCAL_MACHINE` or `LOCAL_MACHINE`
* `CERT_SYSTEM_STORE_LOCAL_MACHINE_GROUP_POLICY` or `LOCAL_MACHINE_GROUP_POLICY`
* `CERT_SYSTEM_STORE_LOCAL_MACHINE_ENTERPRISE` or `LOCAL_MACHINE_ENTERPRISE`
* `CERT_SYSTEM_STORE_CURRENT_SERVICE` or `CURRENT_SERVICE`
* `CERT_SYSTEM_STORE_USERS` or `USERS`
* `CERT_SYSTEM_STORE_SERVICES` or `SERVICES`

```
mimikatz # crypto::stores
Asking for System Store 'CURRENT_USER' (0x00010000)
 0. My
 1. Root
 2. Trust
 3. CA
 4. UserDS
 5. TrustedPublisher
 6. Disallowed
 7. AuthRoot
 8. TrustedPeople
 9. ClientAuthIssuer
10. ACRS
11. SmartCardRoot
```

```
mimikatz # crypto::stores /systemstore:local_machine
Asking for System Store 'local_machine' (0x00020000)
 0. My
 1. Root
 2. Trust
 3. CA
 4. TrustedPublisher
 5. Disallowed
 6. AuthRoot
 7. TrustedPeople
 8. ClientAuthIssuer
 9. FlightRoot
10. TestSignRoot
11. AAD Token Issuer
12. eSIM Certification Authorities
13. Homegroup Machine Certificates
14. Remote Desktop
15. SmartCardRoot
16. TrustedAppRoot
17. TrustedDevices
18. Windows Live ID Token Issuer
19. WindowsServerUpdateServices
```
