# GetUserSPNs.py

[GetUserSPNs.py](https://github.com/SecureAuthCorp/impacket/blob/master/examples/GetUserSPNs.py) can be used to obtain a password hash for user accounts that have an SPN (service principal name). If an SPN is set on a user account it is possible to request a Service Ticket for this account and attempt to crack it in order to retrieve the user password. This attack is named [Kerberoast](https://www.thehacker.recipes/ad/movement/kerberos/kerberoast). This script can also be used for [Kerberoast without preauthentication](https://www.thehacker.recipes/ad/movement/kerberos/kerberoast#kerberoast-w-o-pre-authentication).

## Commons

It has the following generic command line arguments, similar to many other tools:

* required positional argument: `[domain/]username[:password]` (e.g. `domain.local/user`, `domain/user:password`).

![](../../.gitbook/assets/image.png)

* `-hashes`: the LM and/or NT hash to use for a (NTLM). The format is as follows: `[LMhash]:NThash` (the LM hash is optional, the NT hash must be prepended with a colon (`:`).
* `-aesKey`: the AES128 or AES256 hexadecimal long-term key to use for a authentication (Kerberos).
* `-k`: this flag must be set when authenticating using Kerberos. The utility will try to grab credentials from a Ccache file which path must be set in the `KRB5CCNAME` environment variable. In this case, the utility will do . If valid credentials cannot be found or if the `KRB5CCNAME` variable is not or wrongly set, the utility will use the password specified in the positional argument for plaintext Kerberos authentication, or the NT hash (i.e. RC4 long-term key) in the `-hashes` argument for . A Kirbi file could also be converted to a Ccache file using in order to be used by the utility (indirect ).
* `-no-pass`: this flag must be set when an empty password will by used, or no password at all. Without this flag, the user will be prompted for a password when running the utility. This flag is especially useful when using `-k`.
* `-dc-ip`: IP address of the domain controller. If omitted, the positional argument's domain part will be used (in that case, it must be a Fully-Qualified-Domain-Name (FQDN)).
* `-debug`: with this flag set, the utility will be more verbose and will possibly print useful information for debug purposes. With this flag set, the utility will also print tracebacks.
* `-ts`: with this flag set, the utility will prepend all output with a timestamp.

## Specificities

It also has the following specific command line arguments:

* `-request`: the script will retrieve the crackable hash. Without this option, the script will just output vulnerable accounts by identifying the user accounts with an SPN, without actually requesting the TGS.
* `-usersfile`: a file with usernames to test. One username per line must be specified (just the username, no domain needed).
* `-outputfile`: the file name to write the retrieved hashed values in. Without this option set, the values will be printed.
* `-request-user`: requests a Service Ticket for the SPN associated to the specified user (just the username, no domain needed).
* `-save`: saves the requested Service Ticket on the disk, in the `.ccache` format. Useful for [Pass the cache](https://www.thehacker.recipes/ad/movement/kerberos/ptc) attack. This option enables `-request` as well.
* `-target-domain`: allows to specify the domain of the targeted user accounts. It is useful if these accounts are in another domain or forest and the attack is run across a trust. If omitted, the domain specified in the positional argument will be used.
* `-no-preauth`: this option can be used to indicate a user vulnerable to [ASREProast](https://www.thehacker.recipes/ad/movement/kerberos/asreproast), to conduct an [Kerberoast without preauthentication](https://www.thehacker.recipes/ad/movement/kerberos/kerberoast#kerberoast-w-o-pre-authentication) attack.

{% code overflow="wrap" %}
```bash
# with a password
GetUserSPNs.py -outputfile kerberoastables.txt -dc-ip $KeyDistributionCenter 'DOMAIN/USER:Password'

# with an NT hash
GetUserSPNs.py -outputfile kerberoastables.txt -hashes 'LMhash:NThash' -dc-ip $KeyDistributionCenter 'DOMAIN/USER'

# Kerberoast without preauthentication
GetUserSPNs.py -no-preauth "bobby" -usersfile "services.txt" -dc-host "DC_IP_or_HOST" "DOMAIN.LOCAL"/
```
{% endcode %}
