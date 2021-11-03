# backup

`privilege::backup` requests the backup privilege (`SeBackupPrivilege`).

> Required to perform backup operations. This privilege causes the system to grant all read access control to any file, regardless of the [_access control list_](https://docs.microsoft.com/en-us/windows/desktop/SecGloss/a-gly) (ACL) specified for the file. Any access request other than read is still evaluated with the ACL. This privilege is required by the [**RegSaveKey**](https://docs.microsoft.com/en-us/windows/desktop/api/winreg/nf-winreg-regsavekeya) and [**RegSaveKeyEx**](https://docs.microsoft.com/en-us/windows/desktop/api/winreg/nf-winreg-regsavekeyexa)\*\* \*\*functions. The following access rights are granted if this privilege is held:\\
>
> * READ\_CONTROL
> * ACCESS\_SYSTEM\_SECURITY
> * FILE\_GENERIC\_READ
> * FILE\_TRAVERSE
>
> User Right: Back up files and directories.\
> If the file is located on a removable drive and the "Audit Removable Storage" is enabled, the SE\_SECURITY\_NAME is required to have ACCESS\_SYSTEM\_SECURITY.
>
> ([docs.microsoft.com](https://docs.microsoft.com/en-us/windows/win32/secauthz/privilege-constants))

```
mimikatz # privilege::backup
Privilege '17' OK
```
