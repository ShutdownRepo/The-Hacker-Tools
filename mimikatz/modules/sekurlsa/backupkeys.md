# backupkeys

`sekurlsa::backupkeys` lists the preferred Backup Master keys. It has the following command line argument:

* `/export`: save the keys to a file

{% hint style="warning" %}
This command requires elevated privileges (by previously running [`privilege::debug`](../privilege/debug.md) or by executing Mimikatz as the `NT-AUTHORITY\SYSTEM` account).
{% endhint %}

```
mimikatz # sekurlsa::backupkeys

Current prefered key:       {557ab280-17fe-6ce9-8590-52cf907df75e}

Compatibility prefered key: {ad25fae4-a7f2-c7a0-1a9c-4c6f8b5ad34f}
```
