# postzerologon

`lsadump::postzerologon` is a procedure to update AD domain password and its local stored password remotely mimic `netdom resetpwd`. Experimental and best situation after reboot. It has the following command line arguments:

* `/target`: the target domain controller FQDN
* `/account`: the target domain controller's `sAMAccountName`.

{% hint style="warning" %}
Make sure you are aware of the consequences of changing the DC machine account password.
{% endhint %}

```
mimikatz # lsadump::postzerologon /target:192.168.0.10 /account:dc$
```
