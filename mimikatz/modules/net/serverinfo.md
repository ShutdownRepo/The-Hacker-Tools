# serverinfo

`net::serverinfo` displays information about the logged in server

{% tabs %}
{% tab title="Win 10" %}
```
mimikatz # net::serverinfo
platform_id: 500
name       : WIN10
version    : 10.0
comment    :
type       : 00001003 - workstation ; server ; nt ;
```
{% endtab %}

{% tab title="Win Server 2012R2" %}
```
mimikatz # net::serverinfo
platform_id: 500
name       : WIN2012-R2
version    : 6.3
comment    :
type       : 00009003 - workstation ; server ; nt ; server_nt ;
```
{% endtab %}

{% tab title="Win Server 2016 Essentials" %}
```
mimikatz # net::serverinfo
platform_id: 500
name       : DC
version    : 10.0
comment    : My business server
type       : 0080102b - workstation ; server ; domain_ctrl ; time_source ; nt ; dfs ;
```
{% endtab %}
{% endtabs %}
