# name

`privilege::name` requests a privilege by its name. It has the following command line argument:

* positional argument: the name of the privilege

```
mimikatz # privilege::name SeCreateGlobalPrivilege
Privilege '30' OK
```

Below is a list of Windows privileges names:

* `SeTrustedCredManAccessPrivilege`
* `SeNetworkLogonRight`
* `SeTcbPrivilege`
* `SeMachineAccountPrivilege`
* `SeIncreaseQuotaPrivilege`
* `SeInteractiveLogonRight`
* `SeRemoteInteractiveLogonRight`
* `SeBackupPrivilege`
* `SeChangeNotifyPrivilege`
* `SeSystemtimePrivilege`
* `SeTimeZonePrivilege`
* `SeCreatePagefilePrivilege`
* `SeCreateTokenPrivilege`
* `SeCreateGlobalPrivilege`
* `SeCreatePermanentPrivilege`
* `SeCreateSymbolicLinkPrivilege`
* `SeDebugPrivilege`
* `SeDenyNetworkLogonRight`
* `SeDenyBatchLogonRight`
* `SeDenyServiceLogonRight`
* `SeDenyInteractiveLogonRight`
* `SeDenyRemoteInteractiveLogonRight`
* `SeEnableDelegationPrivilege`
* `SeRemoteShutdownPrivilege`
* `SeAuditPrivilege`
* `SeImpersonatePrivilege`
* `SeIncreaseWorkingSetPrivilege`
* `SeIncreaseBasePriorityPrivilege`
* `SeLoadDriverPrivilege`
* `SeLockMemoryPrivilege`
* `SeBatchLogonRight`
* `SeServiceLogonRight`
* `SeSecurityPrivilege`
* `SeRelabelPrivilege`
* `SeSystemEnvironmentPrivilege`
* `SeManageVolumePrivilege`
* `SeProfileSingleProcessPrivilege`
* `SeSystemProfilePrivilege`
* `SeUndockPrivilege`
* `SeAssignPrimaryTokenPrivilege`
* `SeRestorePrivilege`
* `SeShutdownPrivilege`
* `SeSyncAgentPrivilege`
* `SeTakeOwnershipPrivilege`
