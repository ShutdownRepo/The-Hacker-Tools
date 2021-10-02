# stop

It terminates a process by using the [NtTerminateProcess](https://www.geoffchappell.com/studies/windows/win32/ntdll/api/native.htm) Windows Native API function. The Win32 API equal one is [TerminateProcess](https://docs.microsoft.com/en-us/windows/win32/api/processthreadsapi/nf-processthreadsapi-terminateprocess). It has the following command line arguments:

* positional argument: the name of the process to stop
* `/pid`: the PID of the process

In the following example, the `/pid` of `notepad.exe` is `6500`_._

```text
C:\WINDOWS\system32>tasklist /v | findstr notepad
notepad.exe                   6500 RDP-Tcp#4                  4     15,388 K Running         hacklab\m3g9tr0n                                        0:00:00 Untitled - Notepad
```

```text
mimikatz # process::stop notepad /pid:6500
NtTerminateProcess of 6500 PID : OK !
```

