# cng

`crypto::cng` patches the CNG (Cryptography API: Next Generation) service for easy export (Experimental :warning:). This patch modifies `KeyIso` service, in `LSASS` process, in order to make unexportable keys, exportable. This is only useful when the keys provider is `Microsoft Software Key Storage Provider` (you do **not** need to patch `CNG` for other providers). It can be used with [`crypto::certificates`](certificates.md) and [`crypto::keys`](keys.md).

```
mimikatz # privilege::debug
Privilege '20' OK

mimikatz # crypto::cng
"KeyIso" service patched
```
