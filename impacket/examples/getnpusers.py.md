# GetNPUsers.py

[GetNPUsers.py](https://github.com/SecureAuthCorp/impacket/blob/master/examples/GetNPUsers.py) can be used to retrieve domain users who have "Do not require Kerberos preauthentication" set and ask for their TGTs without knowing their passwords. It is then possible to attempt to crack the session key sent along the ticket to retrieve the user password. This attack is known as [ASREProast](https://www.thehacker.recipes/ad/movement/kerberos/asreproast).

{% hint style="info" %}
This script can dynamically obtain the list of users in the domain

* either through an [RPC null session](https://www.thehacker.recipes/ad/recon/ms-rpc#null-sessions)
* or with an authenticated LDAP access to the domain (user or computer account)

If the users list cannot be dynamically retrieved, a file can be supplied.
{% endhint %}

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
* `-ts`: with this flag set, the utility will prepend all output with a timestamp.

## Specificities

It also has the following specific command line arguments:

* `-request`: the script will retrieve the crackable hash. Without this option, the script will just output vulnerable accounts, by identifying if "Do not require Kerberos preauthentication" is set or not, without actually requesting the TGT.
* `-outputfile`: the file name to write the retrieved hashed values in. Without this option set, the values will be printed.
* `-format`: the format to output the hashes in. It must be `hashcat` or `john`. Default is `hashcat` so that the hashes can be ingested by [hashcat](https://tools.thehacker.recipes/hashcat).
* `-usersfile`: a file with usernames to test. One username per line must be specified (just the username, no domain needed). If omitted, the script will automatically identify user accounts with "Do not require Kerberos preauthentication" in the domain via LDAP.

{% hint style="info" %}
If the `-usersfile` argument is not supplied, and no credentials are set (hashes, password, ticket), the script will try to retrieve the users list through the RPC `enumdomusers` command through an [RPC null session](https://www.thehacker.recipes/ad/recon/ms-rpc#null-sessions).
{% endhint %}

{% code overflow="wrap" %}
```bash
# users list dynamically queried with an RPC null session
GetNPUsers.py -request -format hashcat -outputfile ASREProastables.txt -dc-ip $KeyDistributionCenter 'DOMAIN/'

# with a users file
GetNPUsers.py -usersfile users.txt -request -format hashcat -outputfile ASREProastables.txt -dc-ip $KeyDistributionCenter 'DOMAIN/'

# users list dynamically queried with a LDAP authenticated bind (password)
GetNPUsers.py -request -format hashcat -outputfile ASREProastables.txt -dc-ip $KeyDistributionCenter 'DOMAIN/USER:Password'

# users list dynamically queried with a LDAP authenticated bind (NT hash)
GetNPUsers.py -request -format hashcat -outputfile ASREProastables.txt -hashes 'LMhash:NThash' -dc-ip $KeyDistributionCenter 'DOMAIN/USER'
```
{% endcode %}
