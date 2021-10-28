# process

It switches (or reinits) to LSASS process context. It can be used after [`sekurlsa::minidump`](minidump.md).

```
mimikatz # sekurlsa::minidump lsass.dump.dmp
Switch to MINIDUMP : 'lsass.dump.dmp'
```

```
mimikatz # sekurlsa::process
Switch to PROCESS
```
