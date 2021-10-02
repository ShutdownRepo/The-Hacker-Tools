# stop

It stops a specified service by sending a `SERVICE_CONTROL_STOP` signal. It has the following command line argument:

* positional argument: the name of the service to stop

```text
mimikatz # service::stop bits
Stopping 'bits' service : OK
```

{% hint style="warning" %}
The following error might be raised when running this command: `0x00000426 The service has not been started`
{% endhint %}

