# Get-GPPPassword.py

Get-GPPPassword.py can be to used [dump Group Policy Preferences passwords](https://www.thehacker.recipes/ad/movement/credentials/dumping/group-policies-preferences). Unlike other similar tools, this utility doesn't mount the remote `SYSVOL` share from the DC, it uses streams instead to navigate the share and carve file contents.

## Commons

It has the following generic command line arguments, similar to many other tools:

* required positional argument: `[[domain/]username[:password]@]<targetName or address>` or `LOCAL` if the user wants to parse a local file (e.g. `domain.local/user@dc01`, `domain/user:password@10.10.0.1`).

![required positional argument format](<../../.gitbook/assets/impacket\_positional\_arg-with target.png>)

* `-hashes`: the LM and/or NT hash to use for a [pass-the-hash](https://www.thehacker.recipes/ad/movement/ntlm/pth) (NTLM). The format is as follows: `[LMhash]:NThash` (the LM hash is optional, the NT hash must be prepended with a colon (`:`).
* `-aesKey`: the AES128 or AES256 hexadecimal long-term key to use for a [pass-the-key](https://www.thehacker.recipes/ad/movement/kerberos/ptk) authentication (Kerberos).
* `-k`: this flag must be set when authenticating using Kerberos. The utility will try to grab credentials from a Ccache file which path must be set in the `KRB5CCNAME` environment variable. In this case, the utility will do [pass-the-cache](https://www.thehacker.recipes/ad/movement/kerberos/ptc). If valid credentials cannot be found or if the `KRB5CCNAME` variable is not or wrongly set, the utility will use the password specified in the positional argument for plaintext Kerberos authentication, or the NT hash (i.e. RC4 long-term key) in the `-hashes` argument for [overpass-the-hash](https://www.thehacker.recipes/ad/movement/kerberos/opth). A Kirbi file could also be converted to a Ccache file using [ticketConverter.py](ticketconverter.py.md) in order to be used by the utility (indirect [pass-the-ticket](https://www.thehacker.recipes/ad/movement/kerberos/ptt)).
* `-no-pass`: this flag must be set when an empty password will by used, or no password at all. Without this flag, the user will be prompted for a password when running the utility. This flag is especially useful when using `-k`.
* `-dc-ip`: IP address of the domain controller. If omitted, the positional argument's domain part will be used (it must be a Fully-Qualified-Domain-Name (FQDN) though).
* `-debug`: with this flag set, the utility will be more verbose and will possibly print useful information for debug purposes. With this flag set, the utility will also print tracebacks.
* `-ts`: with this flag set, the utility will prepend all output with a timestamp.

## Specificities

It also has the following specific command line arguments:

* `-target-ip`: IP adress of the target machine. If omitted, the positional argument's target part will be used. This argument is useful when NetBIOS name resolution request fail.
* `-port`: remote TCP port the utility must connect to. By default, the port is set to 445 since SMB is the protocol used.
* `-xmlfile`: the path to the local .xml file to parse
* `-share`: the name of the SMB share to search GPP passwords in. By default, this is set to `SYSVOL`.
* `-base-dir`: the directory to search in. By default, this is set to `/`. With a default value in -share, it makes the utility start the search in `\\target\SYSVOL\`.

```bash
# with a NULL session
Get-GPPPassword.py -no-pass 'DOMAIN_CONTROLLER'

# with cleartext credentials
Get-GPPPassword.py 'DOMAIN'/'USER':'PASSWORD'@'DOMAIN_CONTROLLER'

# pass-the-hash (with an NT hash)
Get-GPPPassword.py -hashes :'NThash' 'DOMAIN'/'USER':'PASSWORD'@'DOMAIN_CONTROLLER'

# parse a local file
Get-GPPPassword.py -xmlfile '/path/to/Policy.xml' 'LOCAL'
```
