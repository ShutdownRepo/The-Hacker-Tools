# tpm

`dpapi::tpm` decrypts TPM PCP key file ([Microsoft's TPM Platform Crypto Provider](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/setting-up-tpm-protected-certificates-using-a-microsoft/ba-p/1129055) (PCP)). To check if the device has a Trusted Module TPM Chip:

```
PS C:\WINDOWS\system32> get-tpm


TpmPresent                : True
TpmReady                  : True
ManufacturerId            : 1229870147
ManufacturerIdTxt         : INTC
ManufacturerVersion       : 11.6
ManufacturerVersionFull20 : 11.6.0.1136
ManagedAuthLevel          : Full
OwnerAuth                 : 5lretp/xjie7kWk1wxmX2DZKSrw=
OwnerClearDisabled        : True
AutoProvisioning          : Enabled
LockedOut                 : False
LockoutHealTime           : 2 hours
LockoutCount              : 0
LockoutMax                : 32
SelfTest                  : {}
```

It has the following command line arguments:

* `/in`: the TPM PCP key file
* `/password`: the password to decrypt the tpm key
* `/masterkey`: the masterkey to use for decryption. It can be obtained through [`sekurlsa::dpapi`](https://tools.thehacker.recipes/mimikatz/modules/sekurlsa/dpapi).
* `/unprotect`: display the decryption results on screen

Benjamin has also published a standalone tool called [kirandomtpm](https://github.com/gentilkiwi/kirandomtpm) (C) which is a BCrypt provider to get random bytes from a TPM.

```
mimikatz# dpapi::tpm /unprotect /in:<tpm_file>
```
