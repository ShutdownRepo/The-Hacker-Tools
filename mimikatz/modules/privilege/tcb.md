# tcb

It requests the tcb privilege (`SeTcbPrivilege`).

> This privilege identifies its holder as part of the trusted computer base. Some trusted protected subsystems are granted this privilege.&#x20;
>
> User Right: Act as part of the operating system.
>
> ([docs.microsoft.com](https://docs.microsoft.com/en-us/windows/win32/secauthz/privilege-constants))

```
mimikatz # privilege::tcb
Privilege '7' OK
```

