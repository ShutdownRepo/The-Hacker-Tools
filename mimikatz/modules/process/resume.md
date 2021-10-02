# resume

It resumes a suspended process by using the [NtResumeProcess](https://www.geoffchappell.com/studies/windows/win32/ntdll/api/native.htm) Windows Native API function. It has the following command line arguments:

* positional argument: the name of the process to resume
* `/pid`: the PID of the process

In the following example, the `/pid` of `notepad.exe` is `9212`_._

```text
C:\WINDOWS\system32>tasklist /v | findstr notepad
notepad.exe                   9212 RDP-Tcp#4                  4     15,400 K Running         hacklab\m3g9tr0n                                        0:00:00 Untitled - Notepad
```

```text
mimikatz # process::resume notepad /pid:9212
NtResumeProcess of 9212 PID : OK !
```

