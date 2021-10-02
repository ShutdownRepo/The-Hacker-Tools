# id

It requests a privilege by its `id`. The function used is [RtlAdjustPrivilege](https://www.pinvoke.net/default.aspx/ntdll/RtlAdjustPrivilege.html). This [link](https://docs.microsoft.com/en-us/windows/win32/secauthz/privilege-constants) from MSDN can provide more information for the Privilege Constants. 

In the following example, the `id` of `10` is for `SeLoadDriverPrivilege`:

```text
mimikatz # privilege::id 10
Privilege '10' OK
```

Depending on the defined privilege number, the following error might be encountered:

```text
mimikatz # privilege::id 1
ERROR kuhl_m_privilege_simple ; RtlAdjustPrivilege (1) c0000061

mimikatz # privilege::id 2
ERROR kuhl_m_privilege_simple ; RtlAdjustPrivilege (2) c0000061
```

This indicates that Mimikatz is not running with administrative privileges. UAC is also a case to consider when GUI access is not possible. 

