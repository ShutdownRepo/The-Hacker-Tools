# whoami

`token::whoami` displays the current token.

It has the following argument:

* `/full`: Display more information about groups and privileges. The argument can actually be anything (e.g.`/bar`).

Display current token:

```
mimikatz # token::whoami
 * Process Token : {0;0030f129} 4 F 38912331    SERVER01\tmassie    S-1-5-21-755659916-1915924768-2761631771-1001   (15g,24p)       Primary
 * Thread Token  : no token
```

- For more information about the output, see `token::list``.
- By default, there is no thread token (impersonation token) and only a process token (prmary token).

The `/full` parameter can be used to display more information about groups (`G`) and privileges (`P`):

```
mimikatz # token::whoami /full
 * Process Token : {0;04cfeb5e} 2 F 80775900    client1\tmassie        S-1-5-21-1064812226-1257287110-2416274546-1001  (14g,24p)       Primary
   G:[MDE    ] client1\None
   G:[MDE    ] Everyone
   G:[MDE    ] NT AUTHORITY\Local account and member of Administrators group
   G:[MDE    ] BUILTIN\Users
   G:[MDEO   ] BUILTIN\Administrators
   G:[MDE    ] BUILTIN\Remote Desktop Users
   G:[MDE    ] NT AUTHORITY\INTERACTIVE
   G:[MDE    ] NT AUTHORITY\Authenticated Users
   G:[MDE    ] NT AUTHORITY\This Organization
   G:[MDE    ] NT AUTHORITY\Local account
   G:[MDE  L ] NT AUTHORITY\LogonSessionId_0_624261
   G:[MDE    ] LOCAL
   G:[MDE    ] NT AUTHORITY\NTLM Authentication
   G:[       ] Mandatory Label\High Mandatory Level
   P:[    ]    SeIncreaseQuotaPrivilege
   P:[    ]    SeSecurityPrivilege
   P:[    ]    SeTakeOwnershipPrivilege
   P:[    ]    SeLoadDriverPrivilege
   P:[    ]    SeSystemProfilePrivilege
   P:[    ]    SeSystemtimePrivilege
   P:[    ]    SeProfileSingleProcessPrivilege
   P:[    ]    SeIncreaseBasePriorityPrivilege
   P:[    ]    SeCreatePagefilePrivilege
   P:[    ]    SeBackupPrivilege
   P:[    ]    SeRestorePrivilege
   P:[    ]    SeShutdownPrivilege
   P:[    ]    SeDebugPrivilege
   P:[    ]    SeSystemEnvironmentPrivilege
   P:[DE  ]    SeChangeNotifyPrivilege
   P:[    ]    SeRemoteShutdownPrivilege
   P:[    ]    SeUndockPrivilege
   P:[    ]    SeManageVolumePrivilege
   P:[DE  ]    SeImpersonatePrivilege
   P:[DE  ]    SeCreateGlobalPrivilege
   P:[    ]    SeIncreaseWorkingSetPrivilege
   P:[    ]    SeTimeZonePrivilege
   P:[    ]    SeCreateSymbolicLinkPrivilege
   P:[    ]    SeDelegateSessionUserImpersonatePrivilege
 * Thread Token  : no token
```

Displayed information:

- `*`: Token Type
  - Process Token: Primary Token
  - Thread Token: Impersonation Token
- `G`: Group Information
  - List of assigned groups to the token (source: [kuhl_m_token.c](https://github.com/gentilkiwi/mimikatz/blob/master/mimikatz/modules/kuhl_m_token.c#L155))
  - `M`: Mandatory
  - `D`: Enabled by Default
  - `E`: Group Enabled
  - `O`: Group Owner
  - `U`: Group Use for Deny Only
  - `L`: Group Logon ID
  - `R`: Group Resource
- `P`: Privilege Information
  - List of privileges for this token (source: [kuhl_m_token.c](https://github.com/gentilkiwi/mimikatz/blob/master/mimikatz/modules/kuhl_m_token.c#L226]))
  - `D`: Privilege Enabled by Default
  - `E`: Privilege Enabled
  - `R`: Privilege Removed
  - `A`: Privilege used for Access
