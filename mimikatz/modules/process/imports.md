# imports

It lists all the imported functions from the DLLs each running process is using. If a** **`/pid` is not specified, then imports for `mimikatz.exe` will be displayed. It has the following command line argument:

* `/pid`: the process id

```
mimikatz # process::imports

mimikatz.exe
        00007FF6CAC4F000 -> 00007FFED4047BB0    ADVAPI32.dll ! CryptSetHashParam
        00007FF6CAC4F008 -> 00007FFED4046470    ADVAPI32.dll ! CryptGetHashParam
        00007FF6CAC4F010 -> 00007FFED4046990    ADVAPI32.dll ! CryptExportKey
        00007FF6CAC4F018 -> 00007FFED40471D0    ADVAPI32.dll ! CryptAcquireContextW
        00007FF6CAC4F020 -> 00007FFED405E760    ADVAPI32.dll ! CryptSetKeyParam
        00007FF6CAC4F028 -> 00007FFED405E6E0    ADVAPI32.dll ! CryptGetKeyParam
        00007FF6CAC4F030 -> 00007FFED40475C0    ADVAPI32.dll ! CryptReleaseContext
        00007FF6CAC4F038 -> 00007FFED405E5E0    ADVAPI32.dll ! CryptDuplicateKey
        00007FF6CAC4F040 -> 00007FFED4047090    ADVAPI32.dll ! CryptAcquireContextA
        00007FF6CAC4F048 -> 00007FFED405E700    ADVAPI32.dll ! CryptGetProvParam
        00007FF6CAC4F050 -> 00007FFED4046970    ADVAPI32.dll ! CryptImportKey
        00007FF6CAC4F058 -> 00007FFED1FB3A80    ADVAPI32.dll ! SystemFunction007
        00007FF6CAC4F060 -> 00007FFED405E600    ADVAPI32.dll ! CryptEncrypt
        00007FF6CAC4F068 -> 00007FFED4046A40    ADVAPI32.dll ! CryptCreateHash
        00007FF6CAC4F070 -> 00007FFED405E6A0    ADVAPI32.dll ! CryptGenKey
        00007FF6CAC4F078 -> 00007FFED4046F40    ADVAPI32.dll ! CryptDestroyKey
        00007FF6CAC4F080 -> 00007FFED405E580    ADVAPI32.dll ! CryptDecrypt
        00007FF6CAC4F088 -> 00007FFED4046D00    ADVAPI32.dll ! CryptDestroyHash
        00007FF6CAC4F090 -> 00007FFED4046D20    ADVAPI32.dll ! CryptHashData
        00007FF6CAC4F098 -> 00007FFED4046C10    ADVAPI32.dll ! CopySid
        00007FF6CAC4F0A0 -> 00007FFED40469B0    ADVAPI32.dll ! GetLengthSid
        00007FF6CAC4F0A8 -> 00007FFED404BCC0    ADVAPI32.dll ! LsaQueryInformationPolicy
        00007FF6CAC4F0B0 -> 00007FFED404BCB0    ADVAPI32.dll ! LsaOpenPolicy
        00007FF6CAC4F0B8 -> 00007FFED404BCA0    ADVAPI32.dll ! LsaClose

...Output Omitted...
```
