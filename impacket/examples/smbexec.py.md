# smbexec.py

[smbexec.py](https://github.com/fortra/impacket/blob/master/examples/smbexec.py) can be used to execute commands on a remote Windows target by creating and running a temporary service over **SMB**.  
It provides a semi-interactive shell similar to wmiexec.py and dcomexec.py, but the execution mechanism relies on the **Windows Service Control Manager (SCM)**.

{% hint style="warning" %}
### Required privileges

To use `smbexec.py`, the following prerequisites must be met on the target:

- **Administrative privileges**
- **SMB reachable** (TCP 445 is required for service management and output retrieval)
- **Service Control Manager (SCM) accessible**  
  The authenticated user must be allowed to remotely create/start/delete services (default for local admin)
{% endhint %}

## Commons

It has the following generic command line arguments, similar to other Impacket tools:

* required positional argument:  
  `[[domain/]username[:password]@]<targetName or address>`  
  Examples:  
  - `domain.local/user@dc01`  
  - `domain/user:password@10.10.0.1`

![](<../../.gitbook/assets/impacket\_positional\_arg-with target.png>)

* `-hashes`: the LM and/or NT hash to use for a [pass-the-hash](https://www.thehacker.recipes/ad/movement/ntlm/pth).  
  Format: `[LMhash]:NThash` (LM optional, NT must be prefixed with `:`).

* `-aesKey`: AES128/256 key for [pass-the-key](https://www.thehacker.recipes/ad/movement/kerberos/ptk) authentication (Kerberos).

* `-k`: use Kerberos authentication (via a Ccache if `KRB5CCNAME` is set).

* `-no-pass`: required when no password is provided or when using `-k`.

* `-dc-ip`: IP address of the domain controller to use instead of DNS.

* `-debug`: enables verbose debugging output.

## Specificities

smbexec.py introduces some options specific to the service-based execution model:

* `-codec`: sets the Windows output encoding (default: `latin-1`).  
  Useful for Unicode output on non-English systems.

* `-service-name`: specify a custom service name instead of a random one.

* `-shell-type`: either `cmd` (default) or `powershell`.

* `-keytab`: authenticate using Kerberos keys from a KEYTAB file.

* `-share`: share where the output will be grabbed from (default C$)

* `-mode`: controls how command output is retrieved.  
  - `SHARE` (default): use the existing share specified with `-share` on the target (e.g. `C$`, `ADMIN$`) to store and read command output.  
  - `SERVER`: start a local SMB server on the attacking host and have the target connect back to it to deliver command output.

```bash
# Cleartext authentication
smbexec.py "$DOMAIN"/"$USER":"$PASSWORD"@"$IP"

# Pass-the-hash
smbexec.py -hashes :"$NT_HASH" "$DOMAIN"/"$USER"@"$IP"

# Kerberos authentication
smbexec.py -no-pass -k "$DOMAIN"/"$USER"@"$TARGET"

# PowerShell instead of cmd
smbexec.py -shell-type powershell "$DOMAIN"/"$USER":"$PASSWORD"@"$IP"

# Custom service name
smbexec.py -service-name MyService "$DOMAIN"/"$USER":"$PASSWORD"@"$IP"

# Select share 
smbexec.py -share ADMIN$ "$DOMAIN"/"$USER":"$PASSWORD"@"$IP"
```
