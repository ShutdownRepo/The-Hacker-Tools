# sessions

The module can be used to list the current RDP sessions. It comes in handy for RDP hijacking.

Upon executing `ts::sessions` the following users are identified to be connected over RDP:

* `hacklab\m3g9tr0n` (Session: 3 - RDP-Tcp#4)
* `hacklab\Administrator` (Session: \*4 - RDP-Tcp#5)

```
mimikatz # ts::sessions

Session: 0 - Services
  state: Disconnected (4)
  user :  @
  curr : 9/25/2021 12:41:44 PM
  lock : no

Session: 2 - Console
  state: Connected (1)
  user :  @
  Conn : 9/25/2021 10:45:54 AM
  curr : 9/25/2021 12:41:44 PM
  lock : no

Session: 3 - RDP-Tcp#4
  state: Active (0)
  user : m3g9tr0n @ hacklab
  Conn : 9/25/2021 12:39:48 PM
  disc : 9/25/2021 12:39:48 PM
  logon: 9/25/2021 11:46:55 AM
  last : 9/25/2021 12:40:45 PM
  curr : 9/25/2021 12:41:44 PM
  lock : no
  addr4: 192.168.0.92

Session: *4 - RDP-Tcp#5
  state: Active (0)
  user : administrator @ hacklab
  Conn : 9/25/2021 12:39:49 PM
  disc : 9/25/2021 12:39:49 PM
  logon: 9/25/2021 12:32:36 PM
  last : 9/25/2021 12:41:44 PM
  curr : 9/25/2021 12:41:44 PM
  lock : no
  addr4: 192.168.0.92

Session: 65536 - RDP-Tcp
  state: Listen (6)
  user :  @
  lock : no
```

{% hint style="info" %}
The asterisk on the **Session: \*4 - RDP-Tcp#5 **indicates the user via whom the **ts:sessions** is executed.
{% endhint %}

Another interesting thing to pay attention is the **lock** field (It can be leveraged for RDP lateral movement). When a user has his/her monitor locked, then the following will be displayed:

```
mimikatz # ts::sessions

Session: 3 - RDP-Tcp#4
  state: Active (0)
  user : m3g9tr0n @ hacklab
  Conn : 9/25/2021 12:39:48 PM
  disc : 9/25/2021 12:39:48 PM
  logon: 9/25/2021 11:46:55 AM
  last : 9/25/2021 1:44:53 PM
  curr : 9/25/2021 1:44:57 PM
  lock : yes
  addr4: 192.168.0.92
```

_(Demonstration target is a Windows Server 2016 Essentials)_
