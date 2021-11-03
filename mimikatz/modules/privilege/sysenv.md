# sysenv

`privilege::sysenv` requests the system environment privilege (`SeSystemEnvironmentPrivilege`).

> Required to modify the nonvolatile RAM of systems that use this type of memory to store configuration information.
>
> User Right: Modify firmware environment values.
>
> ([docs.microsoft.com](https://docs.microsoft.com/en-us/windows/win32/secauthz/privilege-constants))

```
mimikatz # privilege::sysenv
Privilege '22' OK
```
