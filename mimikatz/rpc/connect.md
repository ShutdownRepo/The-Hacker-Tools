---
description: Connects to the RPC server
---

# connect

This module can be used to connect to an RPC endpoint. It has the following command line arguments:

* `/alg`: the encryption algorithm to use for the connection. The options are 3DES or RC4. By default it uses 3DES.
* `/remote`: the RPC server to connect
* `/noauth`: no authentication is required to connect to the remote RPC endpoint
* `/authuser`: the user for authentication
* `/authdomain`: the domain of the authuser
* `/authpassword`: the authuser's password

Connect to an RPC server without authentication:

```text
mimikatz # rpc::connect /remote:192.168.0.224 /noauth
[rpc] Remote   : 192.168.0.224
[rpc] ProtSeq  : ncacn_ip_tcp
[rpc] Endpoint : (null)
[rpc] Service  : (null)
[rpc] AuthnSvc : NONE (0)
[rpc] NULL Sess: no
Algorithm: CALG_3DES (00006603)
Endpoint resolution is OK
mimikatz is bound!
```

If the RPC Server was started with an authentication requirement, the `auth*` arguments are needed.

```text
mimikatz # rpc::connect /remote:192.168.0.224 /authuser:m3g9tr0n /authdomain:hacklab.local /authpassword:Super_SecretPass!
[rpc] Remote   : 192.168.0.224
[rpc] ProtSeq  : ncacn_ip_tcp
[rpc] Endpoint : (null)
[rpc] Service  : (null)
[rpc] AuthnSvc : GSS_NEGOTIATE (9)
[rpc] NULL Sess: no
Algorithm: CALG_3DES (00006603)
Endpoint resolution is OK
mimikatz is bound!
```

To run commands on the remote server through the session initiated with mimikatz, a wildcard \(`*`\) should prepend the commands.

```text
mimikatz # hostname
Win10.hacklab.local (WIN10)

mimikatz # *hostname
DC.hacklab.local (DC)
```

The [mimikat](http://mimikatz.py/)[z.py](https://github.com/SecureAuthCorp/impacket/blob/master/examples/mimikatz.py) from impacket can also be used to connect to it:

```text
# python3 mimikatz.py 192.168.0.224                                                                                                                                                                                                     1 ⨯
Impacket v0.9.24.dev1+20210922.102044.c7bc76f8 - Copyright 2021 SecureAuth Corporation


  .#####.   mimikatz RPC interface
 .## ^ ##.  "A La Vie, A L' Amour "
 ## / \ ##  /* * *
 ## \ / ##   Benjamin DELPY `gentilkiwi` ( benjamin@gentilkiwi.com )
 '## v ##'   http://blog.gentilkiwi.com/mimikatz             (oe.eo)
  '#####'    Impacket client by Alberto Solino (@agsolino)    * * */


Type help for list of commands
mimikatz # hostname
DC.hacklab.local (DC)
```

If the remote RPC endpoint requires authentication, then mimikatz.py will need credentials.

```text
# python3 mimikatz.py hacklab.local/m3g9tr0n:Super_SecretPass!@192.168.0.224
Impacket v0.9.24.dev1+20210922.102044.c7bc76f8 - Copyright 2021 SecureAuth Corporation


  .#####.   mimikatz RPC interface
 .## ^ ##.  "A La Vie, A L' Amour "
 ## / \ ##  /* * *
 ## \ / ##   Benjamin DELPY `gentilkiwi` ( benjamin@gentilkiwi.com )
 '## v ##'   http://blog.gentilkiwi.com/mimikatz             (oe.eo)
  '#####'    Impacket client by Alberto Solino (@agsolino)    * * */


Type help for list of commands
mimikatz # hostname
DC.hacklab.local (DC)
```

