# log

It logs mimikatz input/output to a file. It has the following command line arguments:

* positional argument: the filename for the log file (by default it is `mimikatz.log`)
* `/stop`: stop the file logging

```
mimikatz # log
Using 'mimikatz.log' for logfile : OK
```

```
mimikatz # log output.log
Using 'output.log' for logfile : OK
```

```
mimikatz # log /stop
Using '(null)' for logfile : OK
```
