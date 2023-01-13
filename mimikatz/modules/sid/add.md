# add

{% hint style="warning" %}
To use this command, [`sid::patch`](patch.md) must be executed first.
{% endhint %}

`sid::add` can be used to add a SID to `sIDHistory` of an object. The command must be executed directly on a domain controller. It has the following command line argument:

* `/sam`: the `sAMAccountName`.
* `/new`: the new SID value. It also accepts format such as `Builtin\administrators`.

```
mimikatz # sid::add /sam:username /new:Builtin\administrators
```
