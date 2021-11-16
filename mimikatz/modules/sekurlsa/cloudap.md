# cloudap

`sekurlsa::cloudap` lists Azure (Primary Refresh Token) credentials based on the following research: [Digging further into the Primary Refresh Token](https://dirkjanm.io/digging-further-into-the-primary-refresh-token/). [According to Benjamin](https://twitter.com/gentilkiwi/status/1291102498099527682?s=20):

* Azure API does not verify ctx replay
* Azure relies on symmetric keys
* Software or TPM keys are "protected" by legacy DPAPI
* AzureAd logon must support device key for legacy DPAPI

{% hint style="warning" %}
This command requires elevated privileges (by previously running [`privilege::debug`](../privilege/debug.md) or by executing Mimikatz as the `NT-AUTHORITY\SYSTEM` account).
{% endhint %}

```
mimikatz # sekurlsa::cloudap
```

The following screenshot was borrowed from [this tweet](https://twitter.com/\_dirkjan/status/1290397176561119233):

![Azure session key dump](<../../../.gitbook/assets/2 (2).png>)
