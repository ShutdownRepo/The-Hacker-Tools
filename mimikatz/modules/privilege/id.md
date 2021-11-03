# id

`privilege::id` requests a privilege by its `id`.

In the following example, the `id` with value `10` maps to the `SeLoadDriverPrivilege` privilege (like the [driver](driver.md) command).

```
mimikatz # privilege::id 10
Privilege '10' OK
```

Depending on the defined privilege number, the following error might be raised:

```
mimikatz # privilege::id 1
ERROR kuhl_m_privilege_simple ; RtlAdjustPrivilege (1) c0000061

mimikatz # privilege::id 2
ERROR kuhl_m_privilege_simple ; RtlAdjustPrivilege (2) c0000061
```

This indicates that Mimikatz is not running with administrative privileges. UAC is also a case to consider when GUI access is not possible.
