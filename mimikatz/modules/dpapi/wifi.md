# wifi

`dpapi::wifi` decrypts saved Wi-Fi passwords. It has the following command line argument:

* `/in`: The Wlan XML profile. The XML file's location is at `C:\ProgramData\Microsoft\Wlansvc\Profiles\Interfaces\{interface guid}*.xml`
* `/password`: the password to decrypt the Wi-Fi key
* `/masterkey`: the masterkey to use for decryption. It can be obtained through [`sekurlsa::dpapi`](https://tools.thehacker.recipes/mimikatz/modules/sekurlsa/dpapi).
* `/unprotect`: display the decryption results on screen

```
mimikatz # dpapi::wifi /in:"C:\ProgramData\Microsoft\Wlansvc\Profiles\Interfaces\{F4257B8E-3599-4A6F-AEA2-B3B7646ECA80}\{25F4C906-099A-4871-826D-8A604C132954}.xml" /unprotect
Profile 'Timokleia'

 * SSID name     : Timokleia
 * Authentication: WPAPSK
 * Encryption    : AES

**BLOB**
  dwVersion          : 00000001 - 1
  guidProvider       : {df9d8cd0-1501-11d1-8c7a-00c04fc297eb}
  dwMasterKeyVersion : 00000001 - 1
  guidMasterKey      : {f4bff6c3-18ee-435f-b27d-a68e5275389e}
  dwFlags            : 00000000 - 0 ()
  dwDescriptionLen   : 00000002 - 2
  szDescription      :
  algCrypt           : 00006610 - 26128 (CALG_AES_256)
  dwAlgCryptLen      : 00000100 - 256
  dwSaltLen          : 00000020 - 32
  pbSalt             : 4143ac5b363376ee3ad89cf5063ab321fa85df9019fc1cc1c0c440af61df1ea5
  dwHmacKeyLen       : 00000000 - 0
  pbHmackKey         :
  algHash            : 0000800e - 32782 (CALG_SHA_512)
  dwAlgHashLen       : 00000200 - 512
  dwHmac2KeyLen      : 00000020 - 32
  pbHmack2Key        : 69ff3dea262e96881bb300a790574c9703c2d21f1e950cd9d7cd8293a44c4923
  dwDataLen          : 00000010 - 16
  pbData             : e7596546caf68b275814b14bcfce78d0
  dwSignLen          : 00000040 - 64
  pbSign             : c5203a5844b9a00187b76769fadb20e923b502d593c78462c1fb8c5347247e2249772f989160f02a321b4f3c40d1d41dec18af0c417e5279d89728f359a1fde4

 * using CryptUnprotectData API
 * Key Material  : SecureWPAPass
```
