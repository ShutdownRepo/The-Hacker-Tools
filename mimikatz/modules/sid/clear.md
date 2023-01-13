# clear

{% hint style="warning" %}
To use this command, [`sid::patch`](patch.md) must be executed first.
{% endhint %}

`sid::clear` can be used to clear the `sIDHistory` of a target object. The command must be executed directly on a domain controller. It has the following command line argument:

* `/sam`: the `sAMAccountName`.

```
mimikatz # sid::clear /sam:username
```
