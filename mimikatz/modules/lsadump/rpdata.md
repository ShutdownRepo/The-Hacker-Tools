# rpdata

`lsadump::RpData` can retrieve private data (_at the time of writing, Nov 1st 2021, we have no idea what this does or refers to_ :man\_shrugging:). It has the following command line arguments:

* `/export`
* `/secret`
* `/name`
* `/system`

{% hint style="warning" %}
This command requires elevated privileges (by previously running [privilege::debug](https://tools.thehacker.recipes/mimikatz/modules/privilege/debug) or by executing Mimikatz as the `NT-AUTHORITY\SYSTEM` account).
{% endhint %}

```
mimikatz # lsadump::RpData
```
