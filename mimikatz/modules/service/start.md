# start

It starts a service. It has the following command line argument:

* positional argument: the name of the service to start

```text
mimikatz # service::start fax
Starting 'fax' service : OK
```

{% hint style="warning" %}
The following error might be raised when running this command: `0x00000420 An instance of the service is already running`
{% endhint %}

