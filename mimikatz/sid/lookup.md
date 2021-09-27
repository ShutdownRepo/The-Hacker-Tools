# lookup

This module can be used to lookup an object by its SID or name. It has the following command line arguments:

* `/sid`: the security identifier value to lookup
* `/name`: the `sAMAccountName` of the account to lookup
* `/domain`: the domain name. If not specified, the current domain will be used

```text
mimikatz # sid::lookup /name:m3g9tr0n
Name  : m3g9tr0n
Type  : User
Domain: hacklab
SID   : S-1-5-21-2725560159-1428537199-2260736313-1730
```

```text
mimikatz # sid::lookup /sid:S-1-5-21-2725560159-1428537199-2260736313-1730
SID   : S-1-5-21-2725560159-1428537199-2260736313-1730
Type  : User
Domain: hacklab
Name  : m3g9tr0n
```

```text
mimikatz # sid::lookup /sid:S-1-5-21-2725560159-1428537199-2260736313
SID   : S-1-5-21-2725560159-1428537199-2260736313
Type  : Domain
Domain: hacklab
Name  :
```

