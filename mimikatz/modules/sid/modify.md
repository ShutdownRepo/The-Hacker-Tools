# modify

{% hint style="warning" %}
To use this command, [`sid::patch`](patch.md) must be executed first.
{% endhint %}

`sid::modify` can be used to modify an object's SID. The command must be executed directly on a domain controller. It has the following command line argument:

* `/sam`: the `sAMAccountName`.
* `/new`: the new SID value. It also accepts format such as `Builtin\administrators`.

```
mimikatz # sid::modify /sam:username /new:S-1-5-21-...
```

![SID modification](../../../.gitbook/assets/sid\_modify.jpg)
