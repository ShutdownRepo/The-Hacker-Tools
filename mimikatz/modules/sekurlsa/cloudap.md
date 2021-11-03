# cloudap

`sekurlsa::cloudap` lists CloudAp credentials based on the following research: [Digging further into the Primary Refresh Token](https://dirkjanm.io/digging-further-into-the-primary-refresh-token/).

{% hint style="warning" %}
This command requires elevated privileges (by previously running [`privilege::debug`](../privilege/debug.md) or by executing Mimikatz as the `NT-AUTHORITY\SYSTEM` account).
{% endhint %}

```
mimikatz # sekurlsa::cloudap
```

The following screenshot was borrowed from [this tweet](https://twitter.com/\_dirkjan/status/1290397176561119233):

![Azure session key dump](<../../../.gitbook/assets/2 (2).png>)
