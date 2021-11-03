# preshutdown

`service::preshutdown` pre-shuts down a specified service by sending a `SERVICE_CONTROL_PRESHUTDOWN` signal. It has the following command line argument:

* positional argument: the name of the service to shutdown

```
mimikatz # service::shutdown bits
```

{% hint style="warning" %}
The following error might be raised when running this command: `0x00000057 The parameter is incorrect`
{% endhint %}

{% hint style="danger" %}
It must be noted that this command was not found to work on either Windows 7 or Window 10.
{% endhint %}
