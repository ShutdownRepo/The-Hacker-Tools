# blob

`dpapi::blob` describes a DPAPI blob and unprotects/decrypts it with API or Masterkey. It has the following command line arguments:

* `/in`: the path to the blob file
* `/raw`: the blob data in raw format
* `/out`: the path to save the results
* `/ascii`: the blob data in ASCII format
* `/password`: the password to decrypt the blob
* `/unprotect`: displays the decryption results on screen
* `/masterkey`: the masterkey to use for decryption. It can be obtained through [`sekurlsa::dpapi`](https://tools.thehacker.recipes/mimikatz/modules/sekurlsa/dpapi).

```
mimikatz # dpapi::blob /in:dpapi_blob.txt /unprotect
**BLOB**
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
  pbSalt             : 6bccc6a1e6ba8ae74d99fc0801bdc502
  dwHmacKeyLen       : 00000000 - 0
  pbHmackKey         :
  algHash            : 00008004 - 32772 (CALG_SHA1)
  dwAlgHashLen       : 000000a0 - 160
  dwHmac2KeyLen      : 00000010 - 16
  pbHmack2Key        : 2a31aa666d7a0efb8b140df7709d0814
  dwDataLen          : 00000020 - 32
  pbData             : 679f2ed4ef2829dd49f94fb46ebd575b7d545a92d762bbedbf384eece6a69599
  dwSignLen          : 00000014 - 20
  pbSign             : e57681477a7407acceb724c385243070cc7aa6ba

 * using CryptUnprotectData API
description :
data: Hello Mimikatz
```
