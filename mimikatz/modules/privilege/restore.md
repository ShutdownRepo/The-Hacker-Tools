# restore

`privlege::restore` requests the restore privilege (`SeRestorePrivilege`).

> Required to perform restore operations. This privilege causes the system to grant all write access control to any file, regardless of the ACL specified for the file. Any access request other than write is still evaluated with the ACL. Additionally, this privilege enables you to set any valid user or group SID as the owner of a file. This privilege is required by the [**RegLoadKey**](https://docs.microsoft.com/en-us/windows/desktop/api/winreg/nf-winreg-regloadkeya) function. The following access rights are granted if this privilege is held:\\
>
> * WRITE\_DAC
> * WRITE\_OWNER
> * ACCESS\_SYSTEM\_SECURITY
> * FILE\_GENERIC\_WRITE
> * FILE\_ADD\_FILE
> * FILE\_ADD\_SUBDIRECTORY
> * DELETE
>
> User Right: Restore files and directories.\
> If the file is located on a removable drive and the "Audit Removable Storage" is enabled, the SE\_SECURITY\_NAME is required to have ACCESS\_SYSTEM\_SECURITY.
>
> ([docs.microsoft.com](https://docs.microsoft.com/en-us/windows/win32/secauthz/privilege-constants))

```
mimikatz # privilege::restore
Privilege '18' OK
```
