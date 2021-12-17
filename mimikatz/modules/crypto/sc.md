# sc

`crypto::sc` lists smartcard/token reader(s) on, or deported to, the system. When the CSP (Cryptographic Service Provider) is available, it tries to list keys on the smartcard.

```
mimikatz # crypto::sc
SmartCard readers:

 * OMNIKEY CardMan 3x21 0
    ATR  : 3bb794008131fe6553504b32339000d1
    Model: G&D SPK 2.3 T=1
    CSP  : SafeSign Standard Cryptographic Service Provider

 0. 34C99D73A1FAE4D44F9966DF626623DF18858C83
    34C99D73A1FAE4D44F9966DF626623DF18858C83
        Type           : AT_KEYEXCHANGE (0x00000001)
        Exportable key : NO
        Key size       : 1024

 * SCM Microsystems Inc. SCR35xx USB Smart Card Reader 0
```
