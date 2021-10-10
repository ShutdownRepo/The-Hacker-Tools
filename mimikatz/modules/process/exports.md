# exports

It lists all the exported functions from the DLLs each running process is using. If a** **`/pid` is not specified, then exports for `mimikatz.exe` will be displayed. It has the following command line argument:

* `/pid`: the process id

```
mimikatz # process::exports

mimikatz.exe
ntdll.dll
        00007FFED50A11A8 -> 1           00007FFED4FCF110
        00007FFED50A11AC -> 2   0       00007FFED4F90230        A_SHAFinal
        00007FFED50A11B0 -> 3   1       00007FFED4F91060        A_SHAInit
        00007FFED50A11B4 -> 4   2       00007FFED4F910A0        A_SHAUpdate
        00007FFED50A11B8 -> 5   3       00007FFED5030740        AlpcAdjustCompletionListConcurrencyCount
        00007FFED50A11BC -> 6   4       00007FFED4FC0620        AlpcFreeCompletionListMessage
        00007FFED50A11C0 -> 7   5       00007FFED5030770        AlpcGetCompletionListLastMessageInformation
        00007FFED50A11C4 -> 8   6       00007FFED5030790        AlpcGetCompletionListMessageAttributes
        00007FFED50A11C8 -> 9   7       00007FFED4FC0350        AlpcGetHeaderSize
        00007FFED50A11CC -> 10  8       00007FFED4FC0310        AlpcGetMessageAttribute
        00007FFED50A11D0 -> 11  9       00007FFED4F60A60        AlpcGetMessageFromCompletionList
        00007FFED50A11D4 -> 12  10      00007FFED4FD5CA0        AlpcGetOutstandingCompletionListMessageCount
        00007FFED50A11D8 -> 13  11      00007FFED4FC02B0        AlpcInitializeMessageAttribute
        00007FFED50A11DC -> 14  12      00007FFED4FD4900        AlpcMaxAllowedMessageLength
        00007FFED50A11E0 -> 15  13      00007FFED4FD5B20        AlpcRegisterCompletionList
        00007FFED50A11E4 -> 16  14      00007FFED4FC5130        AlpcRegisterCompletionListWorkerThread
        00007FFED50A11E8 -> 17  15      00007FFED4FD5C60        AlpcRundownCompletionList
        00007FFED50A11EC -> 18  16      00007FFED4FD5C80        AlpcUnregisterCompletionList
        00007FFED50A11F0 -> 19  17      00007FFED4FC50D0        AlpcUnregisterCompletionListWorkerThread
        00007FFED50A11F4 -> 20  18      00007FFED4FC6D90        ApiSetQueryApiSetPresence
        00007FFED50A11F8 -> 21  19      00007FFED4FB90A0        ApiSetQueryApiSetPresenceEx
        00007FFED50A11FC -> 22  20      00007FFED4F58D50        CsrAllocateCaptureBuffer
        00007FFED50A1200 -> 23  21      00007FFED4F58D00        CsrAllocateMessagePointer
        00007FFED50A1204 -> 24  22      00007FFED4F58850        CsrCaptureMessageBuffer
        00007FFED50A1208 -> 25  23      00007FFED4F58B40        CsrCaptureMessageMultiUnicodeStringsInPlace
        
...Ouput Omitted...
```

The following output demonstrates a part of the exported functions of the `firefox.exe` process with `3316` PID:

```
mimikatz # process::exports /pid:3516

firefox.exe
        00007FF672034501 -> 2   0       00007FF671FF9D10        GetDependentModulePaths
        00007FF672034505 -> 3   1       00007FF67200B1B0        GetHandleVerifier
        00007FF672034509 -> 4   2       00007FF671FE5110        GetNtLoaderAPI
        00007FF67203450D -> 5   3       00007FF671FFA420        IsSandboxedProcess
        00007FF672034511 -> 6   4       00007FF671FF7970        NativeNtBlockSet_Write
        00007FF672034515 -> 7   5       00007FF67201BA50        TargetConfigureOPMProtectedOutput
        00007FF672034519 -> 8   6       00007FF67201BA20        TargetConfigureOPMProtectedOutput64
        00007FF67203451D -> 9   7       00007FF67201A0A0        TargetCreateNamedPipeW
        00007FF672034521 -> 10  8       00007FF67201A040        TargetCreateNamedPipeW64
        00007FF672034525 -> 11  9       00007FF67201B320        TargetCreateOPMProtectedOutputs
        00007FF672034529 -> 12  10      00007FF67201B2E0        TargetCreateOPMProtectedOutputs64
        00007FF67203452D -> 13  11      00007FF671FF6B50        TargetCreateProcessA
        00007FF672034531 -> 14  12      00007FF67201A3B0        TargetCreateProcessA64
        00007FF672034535 -> 15  13      00007FF671FF6600        TargetCreateProcessW
        00007FF672034539 -> 16  14      00007FF67201A350        TargetCreateProcessW64
        00007FF67203453D -> 17  15      00007FF671FF7190        TargetCreateThread
        00007FF672034541 -> 18  16      00007FF67201A410        TargetCreateThread64
        00007FF672034545 -> 19  17      00007FF67201B580        TargetDestroyOPMProtectedOutput
        00007FF672034549 -> 20  18      00007FF67201B570        TargetDestroyOPMProtectedOutput64

...Output Omitted...
```
