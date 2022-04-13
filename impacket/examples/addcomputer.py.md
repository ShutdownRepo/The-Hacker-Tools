# addcomputer.py

addcomputer.py can be to used to add a new computer account in the Active Directory, using the credentials of a domain user.&#x20;

This is usually done when the [MachineAccountQuota](https://www.thehacker.recipes/ad/movement/domain-settings/machineaccountquota) domain-level attribute is set higher than 0 (set to 10 by default), allowing for standard domain users to create and join machine accounts. Alternatively,if the MachineAccountQuota is 0, the utility can still be used if the credentials used match a powerful enough account (e.g. domain administrator).

The utility can be also used to remove a computer account or change its password if the proper rights are validated.

## Commons

It has the following generic command line arguments, similar to many other tools:

* required positional argument: `[domain/]username[:password]` (e.g. `domain.local/user`, `domain/user:password`).

![](<../../.gitbook/assets/impacket\_positional\_arg-without target.png>)

* `-hashes`: the LM and/or NT hash to use for a [pass-the-hash](https://www.thehacker.recipes/ad/movement/ntlm/pth) (NTLM). The format is as follows: `[LMhash]:NThash` (the LM hash is optional, the NT hash must be prepended with a colon (`:`).
* `-aesKey`: the AES128 or AES256 hexadecimal long-term key to use for a [pass-the-key](https://www.thehacker.recipes/ad/movement/kerberos/ptk) authentication (Kerberos).
* `-k`: this flag must be set when authenticating using Kerberos. The utility will try to grab credentials from a Ccache file which path must be set in the `KRB5CCNAME` environment variable. In this case, the utility will do [pass-the-cache](https://www.thehacker.recipes/ad/movement/kerberos/ptc). If valid credentials cannot be found or if the `KRB5CCNAME` variable is not or wrongly set, the utility will use the password specified in the positional argument for plaintext Kerberos authentication, or the NT hash (i.e. RC4 long-term key) in the `-hashes` argument for [overpass-the-hash](https://www.thehacker.recipes/ad/movement/kerberos/opth). A Kirbi file could also be converted to a Ccache file using [ticketConverter.py](ticketconverter.py.md) in order to be used by the utility (indirect [pass-the-ticket](https://www.thehacker.recipes/ad/movement/kerberos/ptt)).
* `-no-pass`: this flag must be set when an empty password will by used, or no password at all. Without this flag, the user will be prompted for a password when running the utility. This flag is especially useful when using `-k`.
* `-dc-ip`: IP address of the domain controller. If omitted, the positional argument's domain part will be used (in that case, it must be a Fully-Qualified-Domain-Name (FQDN)).
* `-debug`: with this flag set, the utility will be more verbose and will possibly print useful information for debug purposes. With this flag set, the utility will also print tracebacks.

## Specificities

It also has the following specific command line arguments:

* `-dc-host` : hostname of the domain controller. If omitted, the positional argument's domain part will be used (in that case, it must be a Fully-Qualified-Domain-Name (FQDN)).
* `-domain-netbios`: the domain's NetBIOS name where the new computer account will be added. This argument is especially useful when the target forest handles multiple domains.
* `-baseDN`: the distinguished name base in LDAP. If omitted, the positional argument's domain part will be used (in that case, it must be a Fully-Qualified-Domain-Name (FQDN)).
* `-method`: the method to add the new computer account. It can be SAMR to add the account via SMB or LDAPS (default to SAMR). :bulb:_Nota bene: if the chosen method is SAMR, the account will be created without SPNs (Service Principal Names)._
* `-port`: the destination port to connect to. It can be 139, 445 or 636. SAMR defaults to 445, LDAPS to 636.
* `-computer-name`: the name of the new computer account. If omitted, a random `DESKTOP-[A-Z0-9]{8}` name will be used.
* `-computer-pass`: password of the new computer account. If omitted, a random `[A-Za-z0-9]{32}` password will be used. The password will be printed if the computer creation succeeds.
* `-computer-group`: the group to which the new account will be added, with the LDAP path format. If omitted, `CN=Computers` will be used.
* `-no-add`: only changes the specified computer account password without adding a new one.
* `-delete`: deletes an existing computer account.

```bash
# Add a computer account
addcomputer.py -computer-name 'COMPUTER$' -computer-pass 'SomePassword' -dc-host $DomainController -domain-netbios $DOMAIN 'DOMAIN\user:password'

# Modify a computer account password
addcomputer.py -computer-name 'COMPUTER$' -computer-pass 'SomePassword' -dc-host $DomainController -no-add 'DOMAIN\user:password'

# Delete a computer account
addcomputer.py -computer-name 'COMPUTER$' -dc-host $DomainController -delete 'DOMAIN\user:password'
```
