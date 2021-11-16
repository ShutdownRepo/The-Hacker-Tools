# clip

`misc::clip` monitors clipboard. `CTRL+C` stops the monitoring.

```
mimikatz # misc::clip
Monitoring ClipBoard...(CTRL+C to stop)

ClipData: misc::clip
ClipData:

mimikatz #

mimikatz # misc::clip
Monitoring ClipBoard...(CTRL+C to stop)

ClipData:
```

{% hint style="warning" %}
Tests on Windows 10 Enterprise 1903 and 20H2, indicated this didn't work.
{% endhint %}
