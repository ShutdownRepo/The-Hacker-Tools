# smbclient.py

smbclient.py can be used to explore remote SMB shares interactively. It has the following command line arguments:

* required positional argument: `[[domain/]username[:password]@]<targetName or address>` or `LOCAL` if the user wants to parse a local file (e.g. `domain.local/user@dc01`, `domain/user:password@10.10.0.1`).

![required positional argument format](<../../.gitbook/assets/impacket\_positional\_arg-with target.png>)

* `-hashes`: the LM and/or NT hash to use for a [pass-the-hash](https://www.thehacker.recipes/ad/movement/ntlm/pth) (NTLM). The format is as follows: `[LMhash]:NThash` (the LM hash is optional, the NT hash must be prepended with a colon (`:`).
* `-aesKey`: the AES128 or AES256 hexadecimal long-term key to use for a [pass-the-key](https://www.thehacker.recipes/ad/movement/kerberos/ptk) authentication (Kerberos).
* `-k`: this flag must be set when authenticating using Kerberos. The utility will try to grab credentials from a Ccache file which path must be set in the `KRB5CCNAME` environment variable. In this case, the utility will do [pass-the-cache](https://www.thehacker.recipes/ad/movement/kerberos/ptc). If valid credentials cannot be found or if the `KRB5CCNAME` variable is not or wrongly set, the utility will use the password specified in the positional argument for plaintext Kerberos authentication, or the NT hash (i.e. RC4 long-term key) in the `-hashes` argument for [overpass-the-hash](https://www.thehacker.recipes/ad/movement/kerberos/opth). A Kirbi file could also be converted to a Ccache file using [ticketConverter.py](ticketconverter.py.md) in order to be used by the utility (indirect [pass-the-ticket](https://www.thehacker.recipes/ad/movement/kerberos/ptt)).
* `-no-pass`: this flag must be set when an empty password will by used, or no password at all. Without this flag, the user will be prompted for a password when running the utility. This flag is especially useful when using `-k`.
* `-dc-ip`: IP address of the domain controller. If omitted, the positional argument's domain part will be used (it must be a Fully-Qualified-Domain-Name (FQDN) though).
* `-debug`: with this flag set, the utility will be more verbose and will possibly print useful information for debug purposes. With this flag set, the utility will also print tracebacks.
* `-target-ip`: IP adress of the target machine. If omitted, the positional argument's target part will be used. This argument is useful when NetBIOS name resolution request fail.
* `-port`: remote TCP port the utility must connect to. By default, the port is set to 445 since SMB is the protocol used.
* `-file`: input file with commands to execute in the mini shell name of the SMB share to search GPP passwords in. By default, this is set to `SYSVOL`.

Once the interactive SMB shell (a.k.a. minishell) is opened, many cmdlets can be used (non-exhaustive list below):
- `shares`: list available shares.
- `use`: connect to a specific share.
- `ls`: list all the files and directories in the current directory.
- `cd DIR`: change the current directory to.
- `pwd`: show the current directory.
- `rm FILE`: remove a file. The name of the file to remove is expected for this argument.
- `mkdir DIR`: create a directory under the current path.
- `rmdir DIR`: remove a directory under the current path.
- `put FILE`: upload a file into the current path.
- `get FILE`: downloads a file from the current path.
- `mget MASK`: download all files from the current directory matching the provided mask.
- `cat FILE`: read the file from the current path.
- `mount TARGET PATH`: create a mount point from PATH to TARGET (local admin privileges required).
- `umount PATH`: removes the mount point at {path} without deleting the directory (local admin privileges required).
- `list_snapshots PATH`: lists the vss snapshots for the specified path.
- `info`: returns NetrServerInfo main results.
- `who`: returns the sessions currently connected at the target host (local admin privileges required).
- `exit`: terminates the server process (and this session).
- `password`: change the user password, the new password will be prompted for input.

```bash
# (usage example on a domain controller)
smbclient.py 'DOMAIN'/'USER':'PASSWORD'@'DOMAIN_CONTROLLER'
```
```
Type help for list of commands
# shares
ADMIN$
C$
IPC$
NETLOGON
SYSVOL
# use SYSVOL
# ls
drw-rw-rw-          0  Fri Jul  2 15:11:14 2021 .
drw-rw-rw-          0  Fri Jul  2 15:11:14 2021 ..
drw-rw-rw-          0  Fri Jul  2 15:11:14 2021 domain.local
# cd domain.local
# cat domain.local/Policies/{A5C8C37E-9A32-4EA4-AF76-6C094C0117E9}/Machine/Microsoft/Windows NT/SecEdit/GptTmpl.inf
[Unicode]
Unicode=yes
[Version]
signature="$CHICAGO$"
Revision=1
[Group Membership]
*S-1-5-21-1170647656-860703057-891382899-1105__Memberof = *S-1-5-32-544
*S-1-5-21-1170647656-860703057-891382899-1105__Members =

# exit
```


