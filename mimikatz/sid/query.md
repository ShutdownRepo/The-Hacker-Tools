# query

This module can be used to query an object by its SID or name. It has the following command line argument:

* `/sam`: the `sAMAccountName`.

```text
mimikatz # sid::query /sam:m3g9tr0n

CN=m3g9tr0n megas,CN=Users,DC=hacklab,DC=local
  name: m3g9tr0n megas
  objectGUID: {4805c336-f02a-463b-9b3b-94f373759d39}
  objectSid: S-1-5-21-2725560159-1428537199-2260736313-1730
  sAMAccountName: m3g9tr0n
```

