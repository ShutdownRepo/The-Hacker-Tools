# sccm

`misc::sccm` decrypts the password field in the `SC_UserAccount` table in the SCCM database. According to Benjamin (gentilkiwi), the passwords are encrypted with the key embedded in the value (3DES if encounter `0x6603`** **at offset `0x0c`). This key is protected by the `Microsoft Systems Management Server` RSA key but there are many other things like `global secret`, `exchange cert`_, _and some PFX sometimes. It has the following command line arguments:

* `keyuser`: the specific user to target
* `keycontainer`: the exported private key
* `connectionstring`: an example is_ _`DRIVER={SQL Server};Trusted=true;DATABASE=CM_PRD;SERVER=myserver.fqdn\instancename;`.

{% hint style="info" %}
This command requires elevated privileges (by previously running [`privilege::debug`](../privilege/debug.md) or by executing Mimikatz as the `NT-AUTHORITY\SYSTEM` account).
{% endhint %}

{% hint style="info" %}
Based on [Benjamin's suggestion](https://twitter.com/gentilkiwi/status/1399826927112830979?s=20) `misc::sccm` can be run:

* on the SCCM server (with original private key on system and DB access)
* on another system (with private key exported and exported DB - or original)
{% endhint %}

The following image was borrowed from [this tweet](https://twitter.com/gentilkiwi/status/1392204021461569537):

![Decrypt passwords in the SCCM database](<../../../.gitbook/assets/1 (3).PNG>)
