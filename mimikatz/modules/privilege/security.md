# security

`privilege::security` requests the security privilege (`SeSecurityPrivilege`).

> Required to perform a number of security-related functions, such as controlling and viewing audit messages. This privilege identifies its holder as a security operator.
>
> User Right: Manage auditing and security log.
>
> ([docs.microsoft.com](https://docs.microsoft.com/en-us/windows/win32/secauthz/privilege-constants))

```
mimikatz # privilege::security
Privilege '8' OK
```
