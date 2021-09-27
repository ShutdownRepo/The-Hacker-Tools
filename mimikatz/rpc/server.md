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

Start the RPC server without authentication:

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

Start a secure RPC server with authentication:

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

