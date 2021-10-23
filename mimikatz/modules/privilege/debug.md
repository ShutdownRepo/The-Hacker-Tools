# debug

It requests the debug privilege (`SeDebugPrivilege`).

> Required to debug and adjust the memory of a process owned by another account.&#x20;
>
> User Right: Debug programs.
>
> ([docs.microsoft.com](https://docs.microsoft.com/en-us/windows/win32/secauthz/privilege-constants))

```
mimikatz # privilege::debug
Privilege '20' OK
```
