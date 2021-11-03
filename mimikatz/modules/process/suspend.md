# suspend

`process::suspend` suspends a process by using the [NtSuspendProcess](https://ntopcode.wordpress.com/tag/ntsuspendprocess/) Windows Native API function. It has the following command line arguments:

* positional argument: the name of the process to suspend
* `/pid`: the PID of the process

In the following example, the `/pid` of `notepad.exe` is `9212`_._

```
C:\WINDOWS\system32>tasklist /v | findstr notepad
notepad.exe                   9212 RDP-Tcp#4                  4     15,400 K Running         hacklab\m3g9tr0n                                        0:00:00 Untitled - Notepad
```

```
mimikatz # process::suspend notepad /pid:9212
NtSuspendProcess of 9212 PID : OK !
```
