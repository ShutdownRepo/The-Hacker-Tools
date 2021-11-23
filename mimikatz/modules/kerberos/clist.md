# clist

`kerberos::clist` lists tickets in [MIT](https://web.mit.edu/kerberos/)/[Heimdall](https://github.com/heimdal/heimdal) ccache format. It can be useful with other tools (i.e. ones that support [Pass the Cache](https://www.thehacker.recipes/ad/movement/kerberos/ptc)). It has the following command line argument:

* `/export`: export the tickets

```
mimikatz # kerberos::clist
```

{% hint style="warning" %}
At the time of writing, 22nd November 2021, we weren't able to run this command.
{% endhint %}
