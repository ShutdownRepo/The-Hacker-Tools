# list

`process::list` lists all the running processes. It uses the [NtQuerySystemInformation](https://docs.microsoft.com/en-us/windows/win32/api/winternl/nf-winternl-ntquerysysteminformation) Windows Native API function.

```
mimikatz # process::list
4       System
92      Registry
396     smss.exe
492     csrss.exe
608     wininit.exe
736     services.exe
752     lsass.exe
864     svchost.exe
888     fontdrvhost.exe
952     svchost.exe
1000    svchost.exe

...Output Omitted...
```
