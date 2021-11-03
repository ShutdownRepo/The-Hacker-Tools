# suspend

`service::suspend` suspends the specified service. It sends a `SERVICE_CONTROL_PAUSE` signal. It has the following command line argument:

* positional argument: the service name to suspend

```
mimikatz # service::suspend bits
```

{% hint style="warning" %}
Some errors that might be encountered with this command:

* `0x00000426 The service has not been started`
* `0x0000041C The requested control is not valid for this service`
{% endhint %}

{% hint style="danger" %}
It must be noted that this command was not found to work on either Windows 7 or Window 10.
{% endhint %}
